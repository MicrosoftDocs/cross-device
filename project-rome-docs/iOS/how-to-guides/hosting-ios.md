---
title: Hosting cross-device experiences (iOS)
description: This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device.
keywords: microsoft, windows, project rome, iOS api reference 
---

# Hosting cross-device experiences (iOS)

> **Important:** Before you use this guide, make sure you have completed all of the preliminary steps laid out in [Getting started with Connected Devices](getting-started-rome-iOS.md).

This guide shows how to make your app available as a host app that can be remotely launched or provide app service resources to a remote client device. The [Command remote devices and apps](command-remote-devices-and-apps-iOS.md) guide shows how to set up the client side of these actions.

The Project Rome SDK enables scenarios that allow apps to communicate with either an iOS or Android device. This includes the syncing of User Activities on the device as well as launching and messaging. 

## Preliminary setup: push notifications

In addition to the setup steps you have already completed, there are a few more actions you'll need to take to enable your app for hosting scenarios.

Because hosting scenarios often involve waking the device from sleep in order to use the app, it is required that your app be configured to receive push notifications. App launch requests and app service messages will arrive in the form of push notifications, which will then be interpreted accordingly by the platform.

> **Important:** Google and Apple may place limits on the number of notifications that an app can send over their networks in a give period of time. If during app operations it appears that some notifications are not being delivered, it is likely because of this. As we cannot control these policies, this is an issue that the developer must account for in their app.

### Register your app for push notifications

Register your application for [Apple Push Notification](https://developer.apple.com/notifications/) support. Be sure to make note of the sender ID and server key that you receive, since you'll need them later. 

### Register your app form cross-device Connected Devices Platform access

Next, register your app for the [cross-device experiences feature of the Microsoft Developer Dashboard](https://developer.microsoft.com/dashboard/crossplatform/web). This is a different procedure from registering on the Windows Dev Center, which was covered in the [Getting started guide](getting-started-rome-iOS.md). It authorizes the Connected Devices Platform to send notifications using the native push notification service. The Dev Center on-boarding process will require:
* Your app's client ID.
* The Apple Push Notification Service key (for iOS). This is needed in order to deliver data and commands to the app (on a device which may be locked or asleep) in the form of notifications. 

### Configure your app to be notification-compatible

After you complete the workflow on the Developer dashboard, you must modify the actual code of your app to make capable of receiving push notifications. First, make sure to add the "remote-notifications" **UIBackgroundMode** to your app's _Info.plist_, to allow the app to receive notifications while running in the background. 

Second, when your app starts up, you must request authorization to display alert notifications. This is done by calling either `-[UIApplication registerUsernotificationSettings:categories:]` or `-[UNUserNotificationCenter requestAuthorizationWithOptions:completionHandler:]`, depending on what version of iOS you're targeting. Once your app has acquired the authorization, you can then register to receive remote notifications by calling `-[UIApplication registerForRemoteNotifications]`. 

Finally, some notifications from the Connected Devices Platform will present alerts, and the text of these alerts is localizable and must be inserted into your application's string resources. You must define the following resource tags in your app's _en.lproj\Localizable.strings_ file. You may need to create this file. In Xcode, select New > search for the file type "Strings", and create a file called _Localizable.strings_.

```ObjectiveC
/* The text of the toast notification to display when a remote command is received */ 
"ROME_REMOTE_LAUNCH" = "%1$@ wants to launch this app"; 
"ROME_REMOTE_LAUNCH_FROM_APP" = "%1$@ on %2$@ wants to launch this app"; 
 
/* The text of the toast notification to display when multiple remote commands are received simultaneously */ 
"ROME_CONNECT_TEXT_MANY" = "Another device wants to launch this app"; 
```

### Provide the local Platform with access to the notification service

Finally, you must associate push notification functionality with the Connected Devices Platform in your app. In the [Getting started guide](getting-started-rome-iOS.md), you may have initialized the Platform with a `nil` *notificationProvider* parameter. Here, you need to construct and pass in an object that implements **[MCDNotificationProvider](../api-reference/relay/core/MCDNotificationProvider.md)**. The main point of note is the `getNotificationRegistrationAsync:` method, which must return a **[MCDNotificationRegistration](../api-reference/relay/core/MCDNotificationRegistration.md)** instance. The **MCDNotificationRegistration** is responsible for supplying the Connected Devices Platform with an access token (and related information) for the notification service.

You must deliver this registration in your implementation of **MCDNotificationProvider**. Then, the Platform initialization call should provide the local Platform with access to the push notification service, allowing your app to receive data from the server-side Connected Devices Platform, which relays launch requests and app service messages from other devices. 

The following is an implementation of **MCDNotificationProvider** from the sample app.

```Objective-C
@implementation NotificationProvider
{
    MCDRegistrationUpdatedEvent* _registrationUpdated;
    MCDNotificationRegistration* _notificationRegistration;
}

+ (instancetype)sharedInstance
{
    static NotificationProvider* sharedInstance = nil;

    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{ sharedInstance = [[NotificationProvider alloc] init]; });

    return sharedInstance;
}

+ (void)updateNotificationRegistration:(MCDNotificationRegistration*)notificationRegistration
{
    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0),
        ^{ [[NotificationProvider sharedInstance] _updateNotificationRegistration:notificationRegistration]; });
}

// MCDNotificationProvider
@synthesize registrationUpdated = _registrationUpdated;

- (void)getNotificationRegistrationAsync:(nonnull void (^)(MCDNotificationRegistration* _Nullable, NSError* _Nullable))completionBlock
{
    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{ completionBlock(_notificationRegistration, nil); });
}

- (instancetype)init
{
    if (self = [super init])
    {
        _registrationUpdated = [MCDRegistrationUpdatedEvent new];
    }

    return self;
}

- (void)_updateNotificationRegistration:(MCDNotificationRegistration*)notificationRegistration
{
    _notificationRegistration = notificationRegistration;

    [_registrationUpdated raiseWithNotificationRegistration:notificationRegistration];
}
@end
```

The next steps will depend on which scenarios you are targeting. You can set up your app to be remotely launched or to provide an app service. The next two sections will cover these scenarios.

## A) Implement hosting for remote launch
The procedure for making your app available for remote launch centers around the implementation of the **[MCDLaunchUriProvider](../api-reference/relay/hosting/MCDLaunchUriProvider.md)** interface. Add it to the **MCDApplicationRegistration** instance you create in the initial setup, using the **MCDApplicationRegistrationBuilder**'s `setLaunchUriProvider` method. 

The **MCDLaunchUriProvider**'s `onLaunchUriAsync` method passes in a URI along with (optionally) a web-friendly fallback URI and a list of package IDs of apps that are preferred to handle the URI. From here, you can handle the URI in whatever way you have planned for your app. Define the `getSupportedUriSchemes` method to indicate to the system which URI schemes should be delivered to your provider.

## B) Implement hosting for remote app services
The procedure for creating app services that can be accessed by remote devices centers around the implementation of the **[MCDAppServiceProvider](../api-reference/relay/hosting/MCDAppServiceProvider.md)** interface. Add it to the **MCDApplicationRegistration** instance you create in the initial setup, using the **MCDApplicationRegistrationBuilder**'s `addAppServiceProvider` method. 

The **MCDAppServiceProvider**'s `onConnectionOpened` method passes in an **[MCDAppServiceConnection](../api-reference/relay/commanding/MCDAppServiceConnection.md)** representing the connection to the calling app. Use this connection's `addRequestReceivedListener` method to register an event handler for incoming requests. The event handler will receive a **[MCDAppServiceRequestReceivedEventArgs](../api-reference/relay/commanding/MCDAppServiceRequestReceivedEventArgs.md)** object, from which it will get an **[MCDAppServiceRequest](../api-reference/relay/commanding/MCDAppServiceRequest.md)** containing a **NSDictionary** of key/value data. Your app service should handle this data in whatever way is intended and send a response message back using the **MCDAppServiceRequest**'s `sendResponseAsync` method.

