---
title: include file
description: include file
ms.topic: include
ms.assetid: 9fb27596-e9a3-443a-9c12-9e02a893e32c
---


### Associate the Connected Devices Platform with the native push notification for each mobile platform. 

Like previously mentioned, the app clients need to provide knowledge about the native push notification pipeline being used for each mobile platform to the client-side SDK and the Connected Devices Platform during the registration process, to allow Graph notification service to fan-out notifications to each app client endpoint when your app server publishes a user-targeting notification via Microsoft Graph APIs.

In the steps above, you initialized the Platform with a `null` *notificationProvider* parameter. Here, you need to construct and pass in an object that implements **[NotificationProvider](/java/api/com.microsoft.connecteddevices.core._notification_provider)**. The main thing to note is the `getNotificationRegistrationAsync` method, which must return a **[NotificationRegistration](/windows/project-rome/objectivec-api/connecteddevices/mcdconnecteddevicesnotificationregistration)** instance. The **NotificationRegistration** is responsible for supplying the Connected Devices Platform with an access token (and related information) for the notification service.

```java
private NotificationRegistration mNotificationRegistration;

// ...

/**
* NotificationRegistration is constructed with four parameters:
* Type: This is the notification platform type.
* Token: This is the string that GCM or FCM sends to your registration intent service.
* SenderId: This is the numeric Sender ID that you received when you registered your app for push notifications.
* DisplayName: This should be the name of the app that you used when you registered it on the Microsoft dev portal. 
*/
mNotificationRegistration = new NotificationRegistration(NotificationType.FCM, token, FCM_SENDER_ID, "MyAppName");
```

Deliver this registration in your implementation of **NotificationProvider**. Then, the **Platform** initialization call should provide the local **Platform** with access to the push notification service, allowing your app to receive data from the Microsoft Graph Notifications server-side. 

### Pass incoming push notifications to the client SDK
Now, extend your native listener service class ([FirebaseMessagingService](https://firebase.google.com/docs/reference/android/com/google/firebase/messaging/FirebaseMessagingService) in this case, because this tutorial uses Firebase Cloud Messaging) with a special overload of the `onMessageReceived` method (the notification-handling method).

Due to compliance, security, and potential optimizations, the incoming Google Cloud Messaging notification coming from Graph Notifications server-side could be a shoulder tap, which doesn’t contain any data that is initially published by the app server. The retrieval of the actual notification content published by the app server is hidden behind client-side SDK APIs. Because of this, the SDK can provide a consistent programming pattern in which the app client always passes the incoming Google Cloud Messaging payload to the SDK. This allows the SDK to determine whether this is a notification for Connected Device Platform scenarios or not (in case Android’s native Google Cloud Messaging channel is used by the app client for other purposes), and which scenario/capability this incoming notification is corresponding to (Graph Notifications, User Activity, etc.). Specific logics on handling different type of scenarios can then be executed by the app client after that. 

```java
/**
* Check whether it's a Connected Devices Platform notification or not.
* If it is a Connected Devices Platform notification, it will notify the apps with the information in the notification.
* @param from describes message sender.
* @param data message data as String key/value pairs.
*/
@Override
public void onMessageReceived(String from, Bundle data) {
    Log.d(TAG, "From: " + from);

    // Ensure that the Platform is initialized here before going on
    // ...

    // This method passes the data to the Connected Devices Platform if is compatible.
    if (!NotificationReceiver.Receive(data)) {
        // a value of false indicates a non-Rome notification
        Log.d(TAG, "GCM client received a message that was not a Rome notification");
    }
}
```

Your app can now handle notifications from the Connected Devices Platform.
