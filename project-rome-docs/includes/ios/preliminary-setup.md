---
title: include file
description: include file
ms.author: carmenf
author: CarmenForsmann
ms.date: 01/10/2019
ms.topic: include
ms.assetid: 
ms.localizationpriority: medium
---

## Preliminary setup for Connected Devices functionality

Before implementing remote connectivity, there are a few steps you'll need to take to give your iOS app the capability to connect to other remote devices.

### Sign-in

Microsoft Account (MSA) or Azure Active Directory (AAD) authentication is required for all features of the SDK, except for the Nearby sharing APIs. 

If you do not already have an MSA and wish to use one, register on [account.microsoft.com](https://account.microsoft.com/account).

Next, you must register your app with Microsoft by following the instructions on the [Application Registration Portal](https://apps.dev.microsoft.com/) (if you do not have a Microsoft developer account, you must create one first). You should receive a client ID string for your app; save this for later. This will allow your app to access Microsoft's Connected Devices Platform resources. If you're using AAD, see [Azure Active Directory Authentication Libraries](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-libraries) for instructions on getting the client ID string.

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
