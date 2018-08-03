---
title: Hosting cross-device experiences (Android)
description: This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device.
ms.author: pafarley
author: PatrickFarley
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows
ms.technology: connected-devices
keywords: microsoft, windows, project rome, hosting, android
ms.assetid: e96b6e41-f2b2-48fd-906d-eed4b2fbb9a8
ms.localizationpriority: medium
---


# Hosting cross-device experiences (Android)

This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device. The [Command remote devices and apps](../../../commanding/android/how-to-guides/command-remote-devices-and-apps-android.md) guide shows how to set up the client side of these actions.

See the [API reference](../api-reference/index.md) page for links to the reference docs relevant to these scenarios. See the [Android sample app](https://github.com/Microsoft/project-rome/tree/master/Android/samples) for a working example of Project Rome features.

First, initialize the Connected Devices Platform by following the steps below. If you've done this already, skip to the next section.

[!INCLUDE [android/platform-init](../../../includes/android/platform-init.md)]

Next, you must register the application with the Connected Devices Platform cloud directory. If you've done this already, skip to the next section.

[!INCLUDE [android/app-register](../../../includes/android/app-register.md)]

In addition to the setup steps you have already completed, there are a few more actions you'll need to take to enable your app for hosting scenarios.

Because hosting scenarios often involve waking the device from sleep in order to use the app, it is required that your app be configured to receive push notifications. App launch requests and app service messages will arrive in the form of push notifications, which will then be interpreted accordingly by the platform.

> [!IMPORTANT]
> Google and Apple may place limits on the number of notifications that an app can send over their networks in a give period of time. If during app operations it appears that some notifications are not being delivered, it is likely because of this. As we cannot control these policies, this is an issue that the developer must account for in their app.

Follow the steps below to set up push notification support in your app. If you've done this already, skip to the next section.

[!INCLUDE [android/notification-init](../../../includes/android/notification-init.md)]

## Implement a hosting scenario

The next steps will depend on which hosting scenarios you are targeting. You can set up your app to be remotely launched or to provide an app service. The next two sections will cover these scenarios.

### A) Implement hosting for remote launch
The procedure for making your app available for remote launch centers around the implementation of the **[LaunchUriProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.hosting._launch_uri_provider)** interface. Add it to the **ApplicationRegistration** instance you create in the initial setup, using the **ApplicationRegistrationBuilder**'s `setLaunchUriProvider` method. 

The **LaunchUriProvider**'s `onLaunchUriAsync` method passes in a URI along with (optionally) a web-friendly fallback URI and a list of package IDs identifying the apps that are preferred to handle the URI. From here, you can handle the URI in whatever way you have planned for your app. Define the **LaunchUriProvider**'s `getSupportedUriSchemes` method to indicate to the system which URI schemes should be delivered to your provider.

### B) Implement hosting for remote app services
The procedure for creating app services that can be accessed by remote devices centers around the implementation of the **[AppServiceProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.hosting._app_service_provider)** interface. Add it to the **ApplicationRegistration** instance you create in the initial setup, using the **ApplicationRegistrationBuilder**'s `addAppServiceProvider` method. 

The **AppServiceProvider**'s `onConnectionOpened` method passes in an **[AppServiceConnection](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._app_service_connection)** representing the connection to the calling app. Use this connection's `addRequestReceivedListener` method to register an event handler for incoming requests. The event handler will receive an **[AppServiceRequestReceivedEventArgs](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._app_service_request_received_event_args)** object, from which it will get an **[AppServiceRequest](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.commanding._app_service_request)** containing a **Map** of key/value data. Your app service should handle this data in whatever way is intended and send a response message using the **AppServiceRequest**'s `sendResponseAsync` method.

> [!IMPORTANT]
> The **Map**s that are passed between apps and services in the remote app services scenario must adhere to the following format: Keys must be Strings, and the values may be: Strings, boxed numeric types (integers or floating points), boxed booleans, android.graphics.Point, android.graphics.Rect, java.util.Date, java.util.UUID, homogeneous arrays of any of these types, or other **Map** objects that meet this specification.

## Related topics
* [Command remote devices and apps](../../../commanding/android/how-to-guides/command-remote-devices-and-apps-android.md)

