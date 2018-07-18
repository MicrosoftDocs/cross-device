---
title: include file
description: include file
ms.author: pafarley
ms.date: 07/17/2018
ms.topic: include
ms.prod: windows
ms.technology: uwp
ms.assetid: fcbcfd8f-6eea-421a-97bb-31ea3c987728
ms.localizationpriority: medium
---

## Preliminary setup for push notifications

### Register your app for push notifications

Register your application with Google for notification support. Be sure to make note of the sender ID and server key that you receive; you'll need them later. 

### Register your app for cross-device Connected Devices Platform access

Next, register your app for the [cross-device experiences feature of the Microsoft Developer Dashboard](https://developer.microsoft.com/dashboard/crossplatform/web). This is a different procedure from registering on the Windows Dev Center, which was covered in the preliminary steps above. It authorizes the Connected Devices Platform to send notifications using the native push notification service. The Dev Center on-boarding process will require:
* Your app's client ID.
* The Google Cloud Messaging key. This is needed in order to deliver data and commands to the app (on a device which may be locked or asleep) in the form of push notifications. 

### Configure your app to be notification-compatible

After you complete the workflow on the Developer dashboard, you must modify the actual code of your app to make it capable of receiving push notifications. See [Set Up a Firebase Cloud Messaging Client App on Android](https://firebase.google.com/docs/cloud-messaging/android/client) if you are unsure how to do this.

### Associate the notification service with the local Platform

Finally, you must associate push notification functionality with the Connected Devices Platform in your app. In the steps above, you initialized the Platform with a `null` *notificationProvider* parameter. Here, you need to construct and pass in an object that implements **[NotificationProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.core._notification_provider)**. The main thing to note is the `getNotificationRegistrationAsync` method, which must return a **[NotificationRegistration](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.core._notification_registration)** instance. The **NotificationRegistration** is responsible for supplying the Connected Devices Platform with an access token (and related information) for the notification service.


```Java
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

Deliver this registration in your implementation of **NotificationProvider**. Then, the **Platform** initialization call should provide the local **Platform** with access to the push notification service, allowing your app to receive data from the server-side Connected Devices Platform, which relays launch requests and app service messages from other devices. 

All you need to do now is extend your native listener service class ([FirebaseMessagingService](https://firebase.google.com/docs/reference/android/com/google/firebase/messaging/FirebaseMessagingService) in this case, because this guide used Firebase Cloud Messaging) with a special overload of the `onMessageReceived` method (the notification-handling method).

```Java
/**
* Check whether it's a rome notification or not.
* If it is a rome notification, it will notify the apps with the information in the notification.
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

Your app is now able to handle notifications from the Connected Devices Platform.