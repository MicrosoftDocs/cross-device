---
title: AppServiceResponse 
description: Represents a message passed from a remote app service to the client app in response to a previously sent message.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# AppServiceResponse class

```
public class AppServiceResponse
```

Represents a message passed from a remote app service to the client app in response to a previously sent message.


## Methods

### getMessage
`public Map<String, Object> getMessage()`

Retrieves the message sent by the remote app service, consisting of key/value pairs.


#### Returns  
A [Map](https://developer.android.com/reference/java/util/Map.html) object containing String keys mapped to values of variable types.

### getStatus
`public AppServiceResponseStatus getStatus()`

Retrieves the status of the response from the remote app service.


#### Returns  
An [AppServiceResponseStatus](AppServiceResponseStatus.md) value describing the status of the response.

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