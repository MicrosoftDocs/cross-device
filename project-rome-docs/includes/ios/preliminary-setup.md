---
title: include file
description: include file
ms.topic: include
ms.assetid: 
ms.localizationpriority: medium
---

### Register your app

Microsoft Account (MSA) or Azure Active Directory (AAD) authentication is required for almost all features of the Project Rome SDK (the exception being the nearby sharing APIs). If you do not already have an MSA and wish to use one, register on [account.microsoft.com](https://account.microsoft.com/account).

> [!NOTE]
> Azure Active Directory (AAD) accounts are not supported with the Device Relay APIs.

Using your chosen authentication method, you must register your app with Microsoft by following the instructions on the [Application Registration Portal](https://apps.dev.microsoft.com/). If you do not have a Microsoft developer account, you will need to create one.

When you register an app using an MSA, you should receive a client ID string. Save this for later. This will allow your app to access Microsoft's Connected Devices Platform resources. If you're using AAD, see [Azure Active Directory Authentication Libraries](/azure/active-directory/develop/active-directory-authentication-libraries) for instructions on getting the client ID string.

### Add the SDK

The simplest way to add the Connected Devices Platform to your iOS app is by using the [CocoaPods](https://cocoapods.org/) dependency manager. Go to your iOS project's *Podfile* and insert the following entry:

```ObjectiveC
platform :ios, "10.0"
workspace 'iOSSample'

target 'iOSSample' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  # use_frameworks!

	pod 'ProjectRomeSdk'

  # Pods for iOSSample
```

> [!NOTE]
> In order to consume CocoaPod, you must use the _.xcworkspace_ file in your project.