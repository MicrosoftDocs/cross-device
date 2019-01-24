---
title: include file
description: include file
ms.author: lahugh
author: laurenhughes
ms.date: 09/21/2018
ms.topic: include
ms.assetid: dc4d7bbd-bc87-42b1-9924-52c7bfcd5b5f
ms.localizationpriority: medium
---

## Preliminary setup for push notifications

### Register your app for push notifications

Register your application with Google for [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/android/client) support. Be sure to make note of the sender ID and server key that you receive; you'll need them later. 

Once registered, you must associate push notification functionality with the Connected Devices Platform in your app.

```Java
mNotificationRegistration = new ConnectedDevicesNotificationRegistration();
            mNotificationRegistration.setType(ConnectedDevicesNotificationType.FCM);
            mNotificationRegistration.setToken(token);
            mNotificationRegistration.setAppId(Secrets.FCM_SENDER_ID);
            mNotificationRegistration.setAppDisplayName("SampleApp");
```

### Register your app in Microsoft Windows Dev Center for cross-device experiences
If you require communication to your Android device, you need to register your app for the [cross-device experiences feature of the Microsoft Developer Dashboard](https://developer.microsoft.com/dashboard/crossplatform/web). This is a different procedure from MSA and AAD app registration above.  The main goal for this process is to map the platform specific app identities with a cross-platform app identity that is recognized by Connected Devices Platform, and at the same time authorizes the Platform to send notifications using the native push notification services corresponding to each mobile platform. In this case, it enables it enables communication to iOS app endpoints via Firebase Cloud Messaging.

Go to Dev Center Dashboard, navigate to Cross-Device Experiences from the left side navigation pane, and select configuring a new cross-device app, shown as below.
![Dev Center Dashboard – Cross-Device Experiences](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_1_overview.png)

The Dev Center on-boarding process requires the following steps:
* Select supported platforms – select the platforms where your app will have a presence and be enabled for cross-device experiences. You can select from Windows, Android, and/or iOS.
![Cross-Device Experiences – Supported Platforms](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_2_supported_platforms.png)

* Provide app IDs – provide app IDs for each of the platform where your app has a presence. 
![Cross-Device Experiences – App IDs](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_3_app_ids.png)
> [!NOTE]
> You may add different IDs (up to ten) per platform – this is in case you have multiple version of the same app, or even different apps, that want to be able to receive the same notifications sent by your app server targeted at the same user. 
> [!TIP] 
> For Android apps, this is the Package Name you assigned to your app when you created the project. The Package Name can be found in your Firebase console under Project Overview -> General.
![Firebase Console – Project Overview](../../msgraph-notifications/media/dev_center_portal/firebase_overview.png)

* Provide or select the app IDs from MSA and/or AAD app registrations. These client IDs corresponding to MSA or AAD app registration were obtained in the previous MSA/AAD app registration steps from above. 
![Cross-Device Experiences – MSA and AAD App Registrations](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_4_msa_aad_connections.png)

* Connected Devices Platform capabilities leverage each of the native notification platforms on major platforms to send notifications down to the app client endpoints, namely, WNS (for Windows UWP), GCM (for Android) and APNS (for iOS). Provide your credentials for these notification platforms to enable the Platform to deliver the notifications for your app server, when you publish user-targeted notifications.
![Cross-Device Experiences – Push Credentials](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_5_push_credentials.png)
> [!NOTE] 
> For Android, enabling Cloud Messaging service is a prerequisite to communicate with an Android device. See [Set Up a Firebase Cloud Messaging Client App on Android](https://firebase.google.com/docs/cloud-messaging/android/client) for more details. Once you complete the onboarding, you can then provide the push credentials via Windows Dev Center to the Connected Device Platform. 
> [!TIP] 
> The required Sender ID is corresponding to Firebase Cloud Messaging Sender ID, and the API key is corresponding to Legacy Server Key. Both can be found in Firebase Console -> Project -> Settings, under the Cloud Messaging tab, as shown in the screenshot.
![Firebase Console – Android Push Credentials](../../msgraph-notifications/media/dev_center_portal/firebase_push_creds.png)

* The last step is to verify your cross-device app domain, which serves as a verification process to prove that your app has the ownership of this domain which acts like a cross-device app identity for the app you registered.
![Cross-Device Experiences – Domain Verification](../../msgraph-notifications/media/dev_center_portal/dev_center_portal_6_domain_verification.png)

### Process notifications as they are received by the app

Once the Cross-Device experience within the Microsoft Windows Dev Center has been validated, make sure your app can process the notifications as they come in. 

```Java
    ensurePlatformInitialized().thenAccept((ConnectedDevicesPlatform platform) -> {
            ConnectedDevicesProcessNotificationOperation operation = platform.processNotification(data);
        });
```