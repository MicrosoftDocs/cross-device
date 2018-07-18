---
title: Hosting cross-device experiences (iOS)
description: This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device.
ms.author: pafarley
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: microsoft, windows, project rome, hosting, ios
ms.assetid: cd4850df-8ee4-4c44-a26c-f04c29827516
ms.localizationpriority: medium
---


# Hosting cross-device experiences (iOS)

This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device. The [Command remote devices and apps](../../../commanding/ios/how-to-guides/command-remote-devices-and-apps-ios.md) guide shows how to set up the client side of these actions.

See the [API reference](../api-reference/index.md) page for links to the reference docs relevant to these scenarios. See the [iOS sample app](https://github.com/Microsoft/project-rome/tree/master/iOS/samples) for a working example of Project Rome features.

First, initialize the Connected Devices Platform by following the steps below. If you've done this already, skip to the next section.

[!INCLUDE [ios/platform-init](../../../includes/ios/platform-init.md)]

Next, you must register the application with the Connected Devices Platform cloud directory. If you've done this already, skip to the next section.

[!INCLUDE [ios/app-register](../../../includes/ios/app-register.md)]

In addition to the setup steps you have already completed, there are a few more actions you'll need to take to enable your app for hosting scenarios.

Because hosting scenarios often involve waking the device from sleep in order to use the app, it is required that your app be configured to receive push notifications. App launch requests and app service messages will arrive in the form of push notifications, which will then be interpreted accordingly by the platform.

> [!IMPORTANT]
> Google and Apple may place limits on the number of notifications that an app can send over their networks in a give period of time. If during app operations it appears that some notifications are not being delivered, it is likely because of this. As we cannot control these policies, this is an issue that the developer must account for in their app.

Follow the steps below to set up push notification support in your app. If you've done this already, skip to the next section.

[!INCLUDE [ios/notification-init](../../../includes/ios/notification-init.md)]

## Implement a hosting scenario
 
The next steps will depend on which scenarios you are targeting. You can set up your app to be remotely launched or to provide an app service. The next two sections will cover these scenarios.

### A) Implement hosting for remote launch
The procedure for making your app available for remote launch centers around the implementation of the **[MCDLaunchUriProvider](../../../objectivec-api/hosting/MCDLaunchUriProvider.md)** interface. Add it to the **MCDApplicationRegistration** instance you create in the initial setup, using the **MCDApplicationRegistrationBuilder**'s `setLaunchUriProvider` method. 

The **MCDLaunchUriProvider**'s `onLaunchUriAsync` method passes in a URI along with (optionally) a web-friendly fallback URI and a list of package IDs identifying the apps that are preferred to handle the URI. From here, you can handle the URI in whatever way you have planned for your app. Define the **MCDLaunchUriProvider**'s `getSupportedUriSchemes` method to indicate to the system which URI schemes should be delivered to your provider.

## B) Implement hosting for remote app services
The procedure for creating app services that can be accessed by remote devices centers around the implementation of the **[MCDAppServiceProvider](../../../objectivec-api/hosting/MCDAppServiceProvider.md)** interface. Add it to the **MCDApplicationRegistration** instance you create in the initial setup, using the **MCDApplicationRegistrationBuilder**'s `addAppServiceProvider` method. 

The **MCDAppServiceProvider**'s `onConnectionOpened` method passes in an **[MCDAppServiceConnection](../../../objectivec-api/commanding/MCDAppServiceConnection.md)** representing the connection to the calling app. Use this connection's `addRequestReceivedListener` method to register an event handler for incoming requests. The event handler will receive a **`MCDAppServiceRequestReceivedEventArgs`** object, from which it will get an **[MCDAppServiceRequest](../../../objectivec-api/commanding/MCDAppServiceRequest.md)** containing a **NSDictionary** of key/value data. Your app service should handle this data in whatever way is intended and send a response message back using the **MCDAppServiceRequest**'s `sendResponseAsync` method.

> [!IMPORTANT]
> The **NSDictionary** objects that are passed between apps and services in the remote app services scenario must adhere to the following format: Keys must be **NSString**s, and the values may be: **NSString**, boxed numeric types (integers or floating points), boxed booleans, **NSDate**, **NSUUID**, homogeneous arrays of any of these types, or other **NSDictionary** objects that meet this specification. 

## Related topics
* [Command remote devices and apps](../../../commanding/ios/how-to-guides/command-remote-devices-and-apps-ios.md)
