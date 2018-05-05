---
title: Command remote devices and apps (Android)
description: This guide will show how to discover remote devices and apps and then launch apps or interact with app services.
keywords: microsoft, windows, project rome, Android api reference 
---


# Command remote devices and apps (Android)

> **Important:** Before you use this guide, make sure you have completed all of the preliminary steps laid out in [Getting started with Connected Devices](getting-started-rome-android.md).

The commanding scenarios, featured in the Device Relay namespaces, use a watcher pattern in which available devices are detected over time through various types of network connections and corresponding events are raised. This guide will show how to discover remote devices and apps and then launch apps or interact with app services.

## Discover remote devices and apps

A **RemoteSystemWatcher** instance will handle the core functionality of this section.

```Java
private RemoteSystemWatcher mWatcher = null;
```

Before you create a watcher and start discovering devices, you must determine which discovery filters your app will apply. This can be determined by the user or hard-coded into the app, depending on your use case.
```Java
private void onStartWatcherClicked() {
    //RemoteSystemWatcher cannot be started unless the platform is 
    // initialized and the user is logged in. It may be helpful to use
    // methods like these to track the state of the application.
    if (!getMainActivity().isSignedIn()) {
        return;
    }
    if (!getMainActivity().isPlatformInitialized()) {
        return;
    }

    // create a list of filters. Filter choices below are arbitrary.
    ArrayList<RemoteSystemFilter> filters = new ArrayList<>();

    /*  RemoteSystemDiscoveryType filters can be used to filter the types of Remote Systems we discover
    Possible values:
        ANY(0),
        PROXIMAL(1),
        CLOUD(2),
        SPATIALLY_PROXIMAL(3)
    */
    filters.add(new RemoteSystemDiscoveryTypeFilter(RemoteSystemDiscoveryType.ANY));

    /*  RemoteSystemStatusType filters can be used to filter the status of Remote Systems we discover
    Possible values:
        ANY(0),
        AVAILABLE(1)
    */
    filters.add(new RemoteSystemStatusTypeFilter(RemoteSystemStatusType.AVAILABLE));
    

    /*  RemoteSystemKindFilter can filter the types of devices you want to discover.
    Possible values are members of the RemoteSystemKinds class.
    */
    String[] kinds = new String[] { RemoteSystemKinds.Phone(), RemoteSystemKinds.Tablet() };

    RemoteSystemKindFilter kindFilter = new RemoteSystemKindFilter(kinds);
    filters.add(kindFilter);
    

    /*  RemoteSystemAuthorizationKind determines the types of user you want to discover
    Possible values:
        SAME_USER(0),
        ANONYMOUS(1)
    */
    filters.add(new RemoteSystemAuthorizationKindFilter(RemoteSystemAuthorizationKind.SAME_USER)); 
    // ...
```

At this point, the app can initialize the watcher object.

```Java
    // ...
    
    // Create a RemoteSystemWatcher
    // test for empty filters, in case the above code depends on user input.
    if (filters.isEmpty()) {
        mWatcher = new RemoteSystemWatcher();
    } else {
        mWatcher = new RemoteSystemWatcher(filters.toArray(new RemoteSystemFilter[filters.size()]));
    }

    // ...
```

Immediately following the initialization, you should register event handlers for the watcher's events, which is how your app will parse and interact with devices that are discovered. It is recommended that your app maintain a list of discovered devices (represented by **RemoteSystem** instances) and display information about available devices and their apps (such as display name and device type) on the UI. When the registrations are set up, you can create the watcher.

```Java
    // ...

    //Use these events to keep the list of Remote Systems up to date (class definitions below)
    mWatcher.addRemoteSystemAddedListener(new RemoteSystemAddedListener());
    mWatcher.addRemoteSystemUpdatedListener(new RemoteSystemUpdatedListener());
    mWatcher.addRemoteSystemRemovedListener(new RemoteSystemRemovedListener());
    mWatcher.addErrorOccurredListener(new RemoteSystemWatcherErrorOccurredListener());

    // here it is recommended that you clear any old RemoteSystem information from the UI and app memory.
    // ...

    try {
        mWatcher.start();
    } catch (Exception e) { 
        WriteApiException("RemoteSystemWatcher.start", e); 
    }
}

// do not call the above method without defining the watcher's event handlers.
```

The following classes are used as event listeners for the watcher instance.

```Java
private class RemoteSystemAddedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // add instance "remoteSystem" to program memory. See sample for full implementation.
    }
}

private class RemoteSystemUpdatedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // update instance "remoteSystem" in program memory. See sample for full implementation.
    }
}

private class RemoteSystemRemovedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // remove instance "remoteSystem" from program memory. See sample for full implementation.
    }
}

private class RemoteSystemWatcherErrorOccurredListener implements EventListener<RemoteSystemWatcher, RemoteSystemWatcherError> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystemWatcherError remoteSystemWatcherError) {
        // handle the error
    }
}
```

Once `mWatcher.start` is called, it will begin watching for remote system activity and will raise events when connected devices are discovered, updated, or removed from the set of detected devices. It will scan continuously in the background, so it is recommended that you stop the watcher when you no longer need it to avoid unnecessary network communication and battery drain.

```Java
// if you call this from the activity's onPause method, you ensure that
// it will stop when the activity exits the foreground.
public void stopWatcher() {
    if (mWatcher == null) {
        return;
    }
    mWatcher.stop();
}
```

At this point in your code, you should have a working list of **RemoteSystem** objects that refer to available devices. What you do with these devices will depend on the function of your app. The three major types of actions are remote launching, remote app services, and nearby file sharing. They are explained in the following three sections.

## A) Remote launching

The following code shows how to select one of these objects (ideally this is done through a UI control) and then use **RemoteLauncher** to launch an app on it by passing an app-compatible URI. 

It's important to note that a remote launch can target a remote device (in which case the host device will launch the given URI with its default app for that URI scheme) _or_ a specific remote application on that device. 

Depending on the URI that is sent, you can launch an app in a specific state or configuration on a remote device. This allows for the ability to continue a user task, like watching a movie, on a different device without interruption. 

As the previous section demonstrates, discovery happens at the device level first (a **RemoteSystem** represents a device), but you can call the `getApplications` method on a **RemoteSystem** instance to get an array of **RemoteSystemApplication** objects, which represent apps on the remote device that have been registered to use the Connected Devices Platform (just as you registered your own app in the [Getting started guide](getting-started-rome-android.md)). Both **RemoteSystem** and **RemoteSystemApplication** can be used to construct a **RemoteSystemConnectionRequest**, which is what is needed to launch a URI.

```java
// this could be a RemoteSystemApplication instead. Either way, it 
// must be defined somewhere in the application before the launch operation
// is called.
private RemoteSystem target; 

// ...

/**
* Responsible for calling into the Rome API to launch the given URI and provides
* the logic to handle the RemoteLaunchUriStatus response.
* @param uri URI to launch
* @param target The target for the launch URI request
*/
private void launchUri(final String uri, final RemoteSystem target, final long messageId)
{
    RemoteLauncher remoteLauncher = new RemoteLauncher();
    
    AsyncOperation<RemoteLaunchUriStatus> resultOperation = remoteLauncher.launchUriAsync(new RemoteSystemConnectionRequest(target), uri);
    // ...
```
Use the returned **AsyncOperation** to handle the result of the launch attempt.
    
```Java
    // ...
    
    resultOperation.whenCompleteAsync(new AsyncOperation.ResultBiConsumer<RemoteLaunchUriStatus, Throwable>() {
        @Override
        public void accept(RemoteLaunchUriStatus status, Throwable throwable) throws Throwable {
            if (throwable != null) {
                // handle the exception, referencing "throwable"
            } else {
                if (status == RemoteLaunchUriStatus.SUCCESS) {
                    // report the success case
                } else {
                    // report the non-success case, referencing "status"
                }
            }
        }
    });
}
```

Depending on your use, you may need to cover the cases in which no apps on the targeted system can handle the URI, or multiple apps can handle it. The **[RemoteLauncher](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._remote_launcher)** class and **[RemoteLauncherOptions](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._remote_launcher_options)** class describe how to do this.

## B) Remote app services

Your Android app can use the Connected Devices Portal interact with app services on other devices.

This provides many ways to communicate with other devices&mdash;all without needing to bring an app to the foreground of the host device. 

### Set up the app service on the target device
This guide will use the [Roman Test App for Windows](http://aka.ms/romeapp) as its target app service. In other words, the code below will cause an Android app to look for that specific app service on the given remote system. If you wish to test this scenario, download the Roman Test App on a Windows device and make sure you are signed in with the same MSA account you used in the [Getting started guide](getting-started-rome-android.md). 

For instructions on how to write your own UWP app service, see [Create and consume an app service](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service).

If you are writing your own app service on Windows, you will need to make a few edits in order to make the service compatible with Connected Devices. In Visual Studio, go to the app service provider project and select its _Package.appxmanifest_ file. Right-click and select **View Code** to view the full contents of the file. Find the **Extension** element that defines the project as an app service and names its parent project.

``` xml
...
<Extensions>
    <uap:Extension Category="windows.appService" EntryPoint="RandomNumberService.RandomNumberGeneratorTask">
        <uap:AppService Name="com.microsoft.randomnumbergenerator"/>
    </uap:Extension>
</Extensions>
...
```

Change the namespace of the **AppService** element to **uap3** and add the **SupportsRemoteSystems** attribute:

``` xml
...
<uap3:AppService Name="com.microsoft.randomnumbergenerator" SupportsRemoteSystems="true"/>
...
```

In order to use elements in this new namespace, you must add the namespace definition at the top of the manifest file.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3">
  ...
</Package>
```

Build your app service provider project and deploy it to the target device(s).

### Open an app service connection on the client device
Your Android app must acquire a reference to a remote device or application. Like the launch section, this scenario requires the use of a **RemoteSystemConnectionRequest**, which can be constructed from either a **RemoteSystem** or a **RemoteSystemApplication** representing an available app on the system.


```Java
// this could be a RemoteSystemApplication instead. Either way, it 
// must be defined somewhere in the application before the app service
// connection is opened.
private RemoteSystem target = null;

```
Additionally, your app will need to identify its targeted app service by two strings: the *app service name* and *package identifier*. These are found in the source code of the app service provider (see [Create and consume an app service](https://msdn.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service) for details). Together they construct the **AppServiceDescription**, which is fed into an **AppServiceConnection**.

```Java
// this is defined below
private AppServiceConnection connection = null; 


/**
* Creates an AppService connection with the current identifier and service name and opens the
* app service connection.
*/
private void onNewConnectionButtonClicked()
{
    connection = new AppServiceConnection();
    
    // these hard-coded strings must be defined elsewhere in the app
    connection.setAppServiceDescription(new AppServiceDescription(mAppServiceName, mPackageIdentifier));

    // this method is defined below
    openAppServiceConnection();
}
```

So, an **AppServiceConnection** uses a **RemoteSystemConnectionRequest** to determine which remote system or app to target, and it uses its internal **AppServiceDescription** to determine the app service. This is necessary because a single app could provide multiple app services.

```Java
/**
* Establish an app service connection.
* Opens the given AppService connection using the connection request. Once the connection is
* opened, it adds the listeners for request-received and close. Catches all exceptions
* to show behavior of API surface exceptions.
*/
private void openAppServiceConnection()
{
    // optionally report outbound request
    // ...

    RemoteSystemConnectionRequest connectionRequest = new RemoteSystemConnectionRequest(target));

    /*Will asynchronously open the app service connection using the given connection request
    When this is done, we log the traffic in the UI for visibility to the user (for sample purposes)
    We can check the status of the connection to determine whether or not it was successful, and show some UI if it wasn't (in this case it is part of the list item)
    AppServiceConnectionStatus can be as follows:
    SUCCESS(0),
    APP_NOT_INSTALLED(1),
    APP_UNAVAILABLE(2),
    APPSERVICE_UNAVAILABLE(3),
    UNKNOWN(4),
    REMOTE_SYSTEM_UNAVAILABLE(5),
    REMOTE_SYSTEM_NOT_SUPPORTEDBYAPP(6),
    NOT_AUTHORIZED(7)
    */
    connection.openRemoteAsync(connectionRequest)
        .thenAcceptAsync(new AsyncOperation.ResultConsumer<AppServiceConnectionStatus>() {
            @Override
            public void accept(AppServiceConnectionStatus appServiceConnectionStatus) throws Throwable {
                // optionally report inbound response
                // ...

                if (appServiceConnectionStatus != AppServiceConnectionStatus.SUCCESS) {
                    // report the error, referencing "appServiceConnectionStatus"
                    return;
                }
            }
        })
        .exceptionally(new AsyncOperation.ResultFunction<Throwable, Void>() {
            @Override
            public Void apply(Throwable throwable) throws Throwable {
                // report the exception
                return null;
            }
        });
}
```

### Handle connection events

Here, the implementations of the listener interfaces used above are defined. These classes handle connection-related events as well as events that represent response messages from the app service.

```java 
// Define the connection listener class:
class AppServiceConnectionListener implements IAppServiceConnectionListener { 
    
    @Override
    public void onSuccess() {
        Log.i("MyActivityName", "AppServiceConnectionListener onSuccess");
        // connection was successful. initiate messaging or adjust UI to enable a messaging scenario.
    }

    @Override
    public void onError(AppServiceConnectionStatus status) {
        Log.e("MyActivityName", "AppServiceConnectionListener onError status [" + status.toString()+"]");
        // failed to establish connection. inspect the cause of error and reflect back to the UI
    }

    @Override
    public void onClosed(AppServiceConnectionClosedStatus status) {
        Log.i("MyActivityName", "AppServiceConnectionListener onClosed status [" + status.toString()+"]");
        // the connection closed. inspect the cause of closure and reflect back to the UI
    }
} 

// Define the response listener class:
class AppServiceResponseListener implements IAppServiceResponseListener { 
 
    @Override
    public void responseReceived(AppServiceResponse response) {
        AppServiceResponseStatus status = response.getStatus();

        if (status == AppServiceResponseStatus.SUCCESS) {
            // last message was delivered successfully

            Bundle bundle = response.getMessage();
            Log.i("MyActivityName", "Received successful AppService response");
            // parse the expected key/value data stored in "bundle"
        } else {
            Log.e("MyActivityName", "IAppServiceResponseListener.responseReceived status != SUCCESS");
            // inspect "status" for the cause of unsuccessful message delivery
        }
    }
} 
```
### Create a message to send to the app service

On Android, the messages that you send to remote app services will be of the following type.

```Java
private Map<String, Object> mMessagePayload = null;
```
> Note: When your app communicates with app services on other platforms, the Connected Devices Platform translates the **Map** into the equivalent construct on the receiving platform. For example, a **[Map](https://developer.android.com/reference/java/util/Map)** sent from this app to a Windows app service gets translated into a [**ValueSet**](https://msdn.microsoft.com/library/windows/apps/windows.foundation.collections.valueset) object (of the .NET Framework), which can then be interpreted by the app service. Information passed in the other direction undergoes the reverse translation.

The following method crafts a message that can be interpreted by the Roman Test App's app service for Windows.

```Java
/**
* Send the current message payload through all selected AppService connections on a non-UI
* thread as to not block user interaction, a result of the delay between API calls.
*/
private void onMessageButtonClicked()
{
    mMessagePayload = new HashMap<>();
    // Add the required fields of RomanApp on Windows
    DateFormat df = new SimpleDateFormat(DATE_FORMAT);
    mMessagePayload.put("Type", "ping");
    mMessagePayload.put("CreationDate", df.format(new Date()));
    mMessagePayload.put("TargetId", "check if this field needs to be included");

    // this method is defined below.
    sendMessage(connection, mMessagePayload);
}
```

### Send messages to the app service

Once the app service connection is established and the message is created, sending it to the app service is simple and can be done from anywhere in the app that has a reference to the connection instance and the message.


```java

// When assigning message IDs, use an incremental counter
private AtomicInteger mMessageIdAppServices = new AtomicInteger(0);

// ...

/**
* Send a message using the app service connection
* Send the given Map object through the given AppServiceConnection. Uses an internal messageId
* for logging purposes.
* @param connection AppSerivceConnection to send the Map payload
* @param message Payload to be translated to a ValueSet
*/
private void sendMessage(final AppServiceConnection connection, Map<String, Object> message)
{
    final long messageId = mMessageIdAppServices.incrementAndGet();

    connection.sendMessageAsync(message)
        .thenAcceptAsync(new AsyncOperation.ResultConsumer<AppServiceResponse>() {
            @Override
            public void accept(AppServiceResponse appServiceResponse) throws Throwable {
                // optionally report an inbound response

                // this method is defined below
                handleAppServiceResponse(appServiceResponse, messageId);
            }
        })
        .exceptionally(new AsyncOperation.ResultFunction<Throwable, Void>() {
            @Override
            public Void apply(Throwable throwable) throws Throwable {
                // report the exception, referencing "throwable"
                return null;
            }
        });

    // optionally log the outbound message request here, referencing 
    // "connection.getAppServiceDescription().getName()" as the recipient.
}
```

The app service's response will be received and interpreted by the following method.

```Java
private void handleAppServiceResponse(AppServiceResponse appServiceResponse, long messageId)
{
    AppServiceResponseStatus status = appServiceResponse.getStatus();
    if (status == AppServiceResponseStatus.SUCCESS)
    {
        // the message was delivered successfully; interpret the response.
        Map<String, Object> response;
        response = appServiceResponse.getMessage();

        // in the Roman App case, the response contains the date it was
        // created.
        String dateStr = (String)response.get("CreationDate");
        DateFormat df = new SimpleDateFormat(DATE_FORMAT, Locale.getDefault());
        
        // in this very simple use case, we compare the dates to get the total
        // transit time of the message response.
        try {
            Date startDate = df.parse(dateStr);
            Date nowDate = new Date();
            long diff = nowDate.getTime() - startDate.getTime();
        } catch (ParseException e) { e.printStackTrace(); }
    }
}
```
That concludes a single message exchange with a remote app service.

### Finish app service communication

When your app is finished interacting with the target device's app service, close the connection between the two devices.

```java
/**
* Close the given AppService connection
*/
private void closeAppServiceConnection()
{
    connection.close();
}
```


## Related topics
* [Getting started with Connected Devices (Android)](getting-started-rome-android.md)
* [Create and consume an app service](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service).
