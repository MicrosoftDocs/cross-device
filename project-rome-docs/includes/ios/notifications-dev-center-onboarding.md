---
title: include file
description: include file
ms.author: lahugh
author: laurenhughes
ms.date: 09/21/2018
ms.topic: include
ms.assetid: 0741073e-62de-4e31-8e3b-cd1a55027c1c
ms.localizationpriority: medium
---

### Register your app for push notifications

Register your application with Apple for [Apple Push Notification](https://developer.apple.com/notifications/) support. Be sure to make note of the sender ID and server key that you receive; you'll need them later. 

Once registered, you must associate push notification functionality with the Connected Devices Platform in your app.

```ObjectiveC
self.notificationRegistration = [[MCDConnectedDevicesNotificationRegistration alloc] init];
    if ([[UIApplication sharedApplication] isRegisteredForRemoteNotifications])
    {
        self.notificationRegistration.type = MCDNotificationTypeAPN;
    }
    else
    {
        self.notificationRegistration.type = MCDNotificationTypePolling;
    }
    self.notificationRegistration.appId = [[NSBundle mainBundle] bundleIdentifier];
    self.notificationRegistration.appDisplayName = (NSString*)[[NSBundle mainBundle] objectForInfoDictionaryKey:@"CFBundleDisplayName"];
    self.notificationRegistration.token = deviceToken;
    self.isRegisteredWithToken = YES;
```

### Register your app in Microsoft Windows Dev Center for cross-device experiences
If you require communication to your iOS device, you'll need to register with the Microsoft Windows Dev Center.  Next, you need to register your app for the [cross-device experiences feature of the Microsoft Developer Dashboard](https://developer.microsoft.com/dashboard/crossplatform/web). This is a different procedure from MSA and AAD app registration above. The main goal for this process is to map the platform specific app identities with a cross-platform app identity that is recognized by Connected Devices Platform, and at the same time authorizes Microsoft Graph Notifications to send notifications using the native push notification services corresponding to each mobile platform. In this case, it enables Graph Notifications to send notifications to iOS app endpoints via APNS – Apple Push Notification Service. 
Go to Dev Center Dashboard, navigate to Cross-Device Experiences from the left side navigation pane, and select configuring a new cross-device app.
![Dev Center Dashboard – Cross-Device Experiences](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_1_overview.png)

The Dev Center on-boarding process require the following steps:
* Select supported platforms – select the platforms where your app will have a presence and be enabled for cross-device experiences. In the case of Graph Notifications integration, you can select from Windows, Android, and/or iOS.
![Cross-Device Experiences – Supported Platforms](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_2_supported_platforms.png)

* Provide app IDs – provide app IDs for each of the platform where your app has a presence.
![Cross-Device Experiences – App IDs](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_3_app_ids.png)
> [!NOTE]
> You may add different IDs (up to ten) per platform – this is in case you have multiple version of the same app, or even different apps, that want to be able to receive the same notifications sent by your app server targeted at the same user. 
> [!TIP] 
> For iOS apps, this is the Package Name you assigned to your app when you created the project. 

* Provide or select the app IDs from MSA and/or AAD app registrations. These client IDs corresponding to MSA or AAD app registration were obtained in the previous MSA/AAD app registration steps from above.
![Cross-Device Experiences – MSA and AAD App Registrations](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_4_msa_aad_connections.png)
* Graph Notifications and other Connected Devices Platform capabilities leverages each of the native notification platforms on major platforms to send notifications down to the app client endpoints, namely, WNS (for Windows UWP), GCM (for Android) and APNS (for iOS). Provide your credentials for these notification platforms to enable Graph Notifications to deliver the notifications for your app server, when you publish user-targeted notifications. 
![Cross-Device Experiences – Push Credentials](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_5_push_credentials.png)
> [!NOTE] 
> For iOS, enabling APNS is a prerequisite to use Microsoft Graph Notifications. See [APNs Overview](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) for more details. Once you complete the onboarding, you can then provide the push credentials via Windows Dev Center to the Connected Device Platform. 
* The last step is to verify your cross-device app domain, which serves as a verification process to prove that your app has the ownership of this domain which acts like a cross-device app identity for the app you registered.
![Cross-Device Experiences – Domain Verification](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_6_domain_verification.png)
Now you are all set with onboarding! Please proceed to next section. 


