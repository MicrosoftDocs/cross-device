---
title: Hosting cross-device experiences (Android)
description: This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device.
keywords: microsoft, windows, project rome, Android api reference 
---

# Hosting cross-device experiences (Android)

> **Important:** Before you use this guide, make sure you have completed all of the preliminary steps laid out in [Getting started with Connected Devices](getting-started-rome-android.md).

This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device. The [Command remote devices and apps](command-remote-devices-and-apps-android.md) guide shows how to set up the client side of these actions.

The Project Rome SDK enables scenarios that allow apps to communicate with either an Android or iOS device. This includes the syncing of User Activities on the device as well as launching and messaging. 

## Preliminary setup: push notifications

In addition to the setup steps you have already completed, there are a few more actions you'll need to take to enable your app for hosting scenarios.

Because hosting scenarios often involve waking the device from sleep in order to use the app, it is required that your app be configured to receive push notifications. App launch requests and app service messages will arrive in the form of push notifications, which will then be interpreted accordingly by the platform.

> **Important:** Google and Apple may place limits on the number of notifications that an app can send over their networks in a give period of time. If during app operations it appears that some notifications are not being delivered, it is likely because of this. As we cannot control these policies, this is an issue that the developer must account for in their app.

### Register your app for push notifications

Register your application with Google for notification support ([Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) is recommended). Be sure to make note of the sender ID and server key that you receive, since you'll need them later. 

### Register your app form cross-device Connected Devices Platform access

Next, register your app for the [cross-device experiences feature of the Microsoft Developer Dashboard](https://developer.microsoft.com/dashboard/crossplatform/web). This is a different procedure from registering on the Windows Dev Center, which was covered in the [Getting started guide](getting-started-rome-android.md). It authorizes the Connected Devices Platform to send notifications using the native push notification service. The Dev Center on-boarding process will require:
* Your app's client ID.
* The Google Cloud Messaging key (for Android). This is needed in order to deliver data and commands to the app (on a device which may be locked or asleep) in the form of notifications. 

### Configure your app to be notification-compatible

After you complete the workflow on the Developer dashboard, you must modify the actual code of your app to make capable of receiving push notifications. See [Set Up a Firebase Cloud Messaging Client App on Android](https://firebase.google.com/docs/cloud-messaging/android/client) if you are unsure how to do this.

### Provide the local Platform with access to the notification service

Finally, you must associate push notification functionality with the Connected Devices Platform in your app. In the [Getting started guide](getting-started-rome-android.md), you initialized the Platform with a `null` *notificationProvider* parameter. Here, you need to construct and pass in an object that implements **[NotificationProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.core._notification_provider)**. The main point of note is the `getNotificationRegistrationAsync` method, which must return a **[NotificationRegistration](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.core._notification_registration)** instance. The **NotificationRegistration** is responsible for supplying the Connected Devices Platform with an access token (and related information) for the notification service.


```Java
private NotificationRegistration mNotificationRegistration;

// ...

/**
* NotificationRegistration is constructed with four parameters:
* Type: This is GCM or FCM or APN (the notification platform type).
* Token: This is the string that GCM or FCM sends to your registration intent service.
*SenderId: This is the numeric Sender ID that you received when you registered your app for push notifications.
* DisplayName: This should be the name of the app that you used when you registered it on the Microsoft dev portal. 
*/
mNotificationRegistration = new NotificationRegistration(NotificationType.FCM, token, FCM_SENDER_ID, "MyAppName");
```

Deliver this registration in your implementation of **NotificationProvider**. Then, the Platform initialization call should provide the local Platform with access to the push notification service, allowing your app to receive data from the server-side Connected Devices Platform, which relays launch requests and app service messages from other devices. 

All you need to do now is extend your listener service class ([FirebaseMessagingService](https://firebase.google.com/docs/reference/android/com/google/firebase/messaging/FirebaseMessagingService) in this case, because this guide used FCM) with a special overload of the `onMessageReceived` method (the notification-receiving method).

```Java
/**
* Check whether it's a rome notification or not.
* If it is a rome notification,
* It will notify the apps with the information in the notification.
* @param  from  describes message sender.
* @param  data  message data as String key/value pairs.
*/
@Override
public void onMessageReceived(String from, Bundle data) {
    Log.d(TAG, "From: " + from);

    // Ensure that the Platform is initialized here before going on
    // ...

    // call NotificationReceiver.Receive(data), which passes the data to 
    // the Platform if is compatible.
    if (!NotificationReceiver.Receive(data)) {
        Log.d(TAG, "GCM client received a message that was not a Rome notification");
    }
}
```


The next steps will depend on which scenarios you are targeting. You can set up your app to be remotely launched or to provide an app service. The next two sections will cover these scenarios.

## A) Implement hosting for remote launch
The procedure for making your app available for remote launch centers around the implementation of the **[LaunchUriProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.hosting._launch_uri_provider)** interface. Add it to the **ApplicationRegistration** instance you create in the initial setup, using the **ApplicationRegistrationBuilder**'s `setLaunchUriProvider` method. 

The **LaunchUriProvider**'s `onLaunchUriAsync` method passes in a URI along with (optionally) a web-friendly fallback URI and a list of package IDs of apps that are preferred to handle the URI. From here, you can handle the URI in whatever way you have planned for your app. Define the `getSupportedUriSchemes` method to indicate to the system which URI schemes should be delivered to your provider.

## B) Implement hosting for remote app services
The procedure for creating app services that can be accessed by remote devices centers around the implementation of the **[AppServiceProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.hosting._app_service_provider)** interface. Add it to the **ApplicationRegistration** instance you create in the initial setup, using the **ApplicationRegistrationBuilder**'s `addAppServiceProvider` method. 

The **AppServiceProvider**'s `onConnectionOpened` method passes in an **[AppServiceConnection](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._app_service_connection)** representing the connection to the calling app. Use this connection's `addRequestReceivedListener` method to register an event handler for incoming requests. The event handler will receive a **[AppServiceRequestReceivedEventArgs](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._app_service_request_received_event_args)** object, from which it will get an **[AppServiceRequest](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._app_service_request)** containing a **Map** of key/value data. Your app service should handle this data in whatever way is intended and send a response message back using the **AppServiceRequest**'s `sendResponseAsync` method.

> **Note:** The **Map**s that are passed between apps and services in the remote app services scenario must adhere to the following format: Keys must be Strings, and the values may be: Strings, boxed numeric types (integers or floating points), boxed booleans, android.graphics.Point, android.graphics.Rect, java.util.Date, java.util.UUID, homogeneous arrays of any of these types, or other **Map** objects that meet this specification.

