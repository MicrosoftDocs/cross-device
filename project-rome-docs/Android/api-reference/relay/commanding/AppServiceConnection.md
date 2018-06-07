---
title: AppServiceConnection 
description: This class manages a connection to a particular remote app service.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# AppServiceConnection class

```
public final class AppServiceConnection
```

This class manages a connection to a particular remote app service.

## Constructors

### AppServiceConnection
`public AppServiceConnection(@NonNull AppServiceDescription appServiceDescription)`

Initializes an instance of this class.

#### Parameters
* `appServiceDescription` [optional] Describes the app service to target in this connection.

## Methods

### close 
`public void close()`

Closes the connection to the remote app service. The client app should call this method whenever it is closed or stopped by the user or system.

### openRemoteAsync
`public AsyncOperation<AppServiceConnectionStatus> openRemoteAsync(@NonNull RemoteSystemConnectionRequest connection)`

Opens the app service connection on the specified remote device or application. If the connection fails to open, an exception is thrown.

>**Note:** This method will thrown an exception if any of the following are true:
> * The connection is already open or is in the process of opening.
> * The app service description has not been set or has been cleared.
> * The platform has not been initialized.
> * The app has subscribed a method to the connection's "request received" event but has not provided a **NotificationProvider** when initializing the platform. All hosting scenarios require a **NotificationProvider**.

#### Parameters 
* `connection` The connection request, which specifies the device or application to connect to. 

#### Returns
An asynchronous operation with an [AppServiceConnectionStatus](AppServiceConnectionStatus.md) indicating the status of the attempted connection.

#### sendMessageAsync
`public AsyncOperation<AppServiceResponse> sendMessageAsync(@NonNull Map<String, Object> messageMap)`

Sends a message to the remote app service and begins listening for a response. This method should only be called after the connection was opened successfully.

#### Parameters
* `messageMap` a Map of the keys and values to send.

#### Returns
An asynchronous operation with an [AppServiceResponse](AppServiceResponse.md) object, which represents the remote app service's response to the message being sent.

### getAppServiceDescription
`public AppServiceDescription getAppServiceDescription()`

Gets details about the target app service to connect to.

#### Returns  
The description object of the target app service.


### setAppServiceDescription
`public void setAppServiceDescription(@NonNull AppServiceDescription appServiceDescription)`

Specifies the target app service to connect to.

#### Parameters
appServiceDescription - the description object for the app service.

### addRequestReceivedListener
`public long addRequestReceivedListener(@NonNull EventListener<AppServiceConnection, AppServiceRequestReceivedEventArgs> listener)`

Assigns an event listener to this **AppServiceConnection**, to handle the event in which a service request is received from a remote app.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
A unique identifier for this event listener. This is needed to remove the listener from this event.

### removeRequestReceivedListener
`public void removeRequestReceivedListener(long eventRegistrationToken)`

Removes a previously assigned "request received" event listener from this **AppServiceConnection**.

#### Parameters
* `eventRegistrationToken` The unique identifier of the "request received" event listener to be removed.

### addServiceClosedListener
`public long addServiceClosedListener(@NonNull EventListener<AppServiceConnection, AppServiceClosedStatus> listener)`

Assigns an event listener to this **AppServiceConnection**, to handle the event in which the connection to the app service closes.

> **Note:** On the client app, the "app service closed" event is only raised for unexpected connection interruptions; it is not raised when the `close` method is called by either the client or the host. On the host app, the event _is_ raised when the client calls `close`.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
A unique identifier for this event listener. This is needed to remove the listener from this event.

### removeServiceClosedListener
Removes a previously assigned "service closed" event listener from this **AppServiceConnection**.

`public void removeServiceClosedListener(long eventRegistrationToken)`

#### Parameters
* `eventRegistrationToken` The unique identifier of the "service closed" event listener to be removed.

## Example

The following sample code lays out the basic steps of opening a connection to a remote app service, sending a message, and receiving a response.

```Java

/**
    * Preliminary: Create an AppService connection with the current identifier and service name and open the
    * app service connection.
    */
private void onNewConnectionButtonClicked()
{
    connection = new AppServiceConnection();
    // these description strings must be acquired beforehand
    connection.setAppServiceDescription(new AppServiceDescription(mAppServiceName, mPackageIdentifier));

    // method defined below
    openAppServiceConnection();
}

/**
* Step #1:  Establish an app service connection
* Opens the given AppService connection using the connection request. Once the connection is
* opened, it adds the listeners for request received and close. Catches all exceptions and
* prints them to show behavior of API surface exceptions.
*/
private void openAppServiceConnection()
{
    String title = String.format("Outbound open connection request");
    mLogList.logTraffic(title);

    // the RemoteSystemApplication "mRemoteSystemApplication" must be
    // set beforehand
    RemoteSystemConnectionRequest connectionRequest = mRemoteSystemApplication.getRemoteSystemConnectionRequest();

    /*Will asynchronously open the app service connection using the given connection request
    When this is done, we log the traffic in the UI for visibility to the user (for sample purposes)
    We can check the status of the connection to determine whether or not it was successful, and show some UI if it wasn't (in this case it is part of the list item)
    */
    connection.openRemoteAsync(connectionRequest)
            .thenAcceptAsync(new AsyncOperation.ResultConsumer<AppServiceConnectionStatus>()
            {
                @Override
                public void accept(AppServiceConnectionStatus appServiceConnectionStatus) throws Throwable {
                    String title = "Inbound open connection response";
                    mLogList.logTraffic(title);

                    if (appServiceConnectionStatus != AppServiceConnectionStatus.SUCCESS) {
                        Log.d("LaunchFragment", "App Service Connection failed: " + appServiceConnectionStatus.toString());
                        return;
                    }
                }
            })
            .exceptionally(new AsyncOperation.ResultFunction<Throwable, Void>() {
                @Override
                public Void apply(Throwable throwable) throws Throwable {
                    WriteApiException("AsyncOperation<AppServiceConnectionStatus>.get", throwable);
                    return null;
                }
            });
}

// Step #2:  Create a message to send in the form of a Map<String, Object>. 
// This will depend on the app service and what kind of data it accepts.

/**
* Step #3:  Send a message using the app service connection
* Send the given Map object through the given AppService connection. Uses an internal messageId
* for logging purposes.
* @param connection AppService connection to send the Map payload
* @param message Payload to be translated to a ValueSet
*/
private void sendMessage(final AppServiceConnection connection, Map<String, Object> message)
{
    // the message ID is acquired elsewhere in the application
    final long messageId = mMessageIdAppServices.incrementAndGet();

    // attempt to send the message.
    connection.sendMessageAsync(message)
            .thenAcceptAsync(new AsyncOperation.ResultConsumer<AppServiceResponse>() {
                @Override
                public void accept(AppServiceResponse appServiceResponse) throws Throwable {
                    String title = "Inbound message response";
                    mLogList.logTraffic(title);

                    // method defined below
                    handleAppServiceResponse(appServiceResponse, messageId);
                }
            })
            .exceptionally(new AsyncOperation.ResultFunction<Throwable, Void>() {
                @Override
                public Void apply(Throwable throwable) throws Throwable {
                    WriteApiException("SendMessageAsync AsyncOperation<AppServiceResponse>.get", throwable);
                    return null;
                }
            });

    // Construct the traffic log message and log it
    String title = "Outbound message request to " + connection.getAppServiceDescription().getName();
    mLogList.logTraffic(title);
}


/**
* Step #4:  Get a response message
* Provides the logic for how to handle the response to an AppService request message. This example looks for
* a field containing the date to calculate the round-trip time of the message.
* @param appServiceResponse
* @param messageId
*/
private void handleAppServiceResponse(AppServiceResponse appServiceResponse, long messageId)
{
    AppServiceResponseStatus status = appServiceResponse.getStatus();
    if (status == AppServiceResponseStatus.SUCCESS)
    {
        Map<String, Object> response;

        response = appServiceResponse.getMessage();

        String dateStr = (String)response.get("CreationDate");
        DateFormat df = new SimpleDateFormat(DATE_FORMAT, Locale.getDefault());
        try {
            Date startDate = df.parse(dateStr);
            Date nowDate = new Date();
            long diff = nowDate.getTime() - startDate.getTime();

        } catch (ParseException e) { e.printStackTrace(); }
    }
}
```