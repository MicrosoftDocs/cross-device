### Associate the Connected Devices Platform with the native push notification for each platform. 

Like previously mentioned, the app clients need to provide knowledge about the native push notification pipeline being used for each platform to the client-side SDK and the Connected Devices Platform during the registration process, in order to allow Graph notification service to fan-out notifications to each app client endpoint when your app server publishes a user-targeting notification via MS Graph APIs.
In the steps above, you initialized the Platform without **NotificationProvider** parameter. Here, you need to construct and pass in an object that implements **NotificationProvider**. Please see **GraphNotificationProvider.cs** from sample for details. 



Deliver this registration in your implementation of **NotificationProvider**. Then, the **Platform** initialization call should provide the local **Platform** with access to the push notification service, allowing your app to receive data from the MS Graph Notifications server-side. 

### Pass incoming push notifications to the client SDK
Now, you can handle incoming UserNotification payload inside the Windows native background task registered with PushNotificationTrigger, or in your listner of the [PushNotificationReceived event](https://docs.microsoft.com/en-us/uwp/api/windows.networking.pushnotifications.pushnotificationchannel.pushnotificationreceived). 

For reasons including compliance, security, and potential optimizations, the incoming WNS raw notification coming from Graph Notifications server-side could often be a shoulder tap which doesn’t contain any data that is initially published by the app server. The retrieval of the actual notification content published by app server is hidden behind client-side SDK APIs. In this case, the SDK always asks the app client to pass the incoming WNS raw notification payload to the SDK. This allows the SDK to determine whether this is a notification for Graph Notifications scenarios or not (in case WNS raw push can also be used by the app client for other purposes). 
