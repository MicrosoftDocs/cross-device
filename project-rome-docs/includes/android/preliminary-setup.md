---
title: include file
description: include file
ms.topic: include
ms.assetid: 
ms.localizationpriority: medium
---

## Preliminary setup for the Connected Devices Platform and Notifications

Before implementing remote connectivity, there are a few steps you'll need to take to give your Android app the capability to connect to remote devices as well as send and receive notifications.

### Register your app

Microsoft Account (MSA) or Azure Active Directory (AAD) authentication is required for almost all features of the Project Rome SDK (the exception being the nearby sharing APIs). If you do not already have an MSA and wish to use one, register on [account.microsoft.com](https://account.microsoft.com/account).

> [!NOTE]
> Azure Active Directory (AAD) accounts are not supported with the Device Relay APIs.

Using your chosen authentication method, you must register your app with Microsoft by following the instructions on the [Application Registration Portal](https://apps.dev.microsoft.com/). If you do not have a Microsoft developer account, you will need to create one.

When you register an app using an MSA, you should receive a client ID string. Save this for later. This will allow your app to access Microsoft's Connected Devices Platform resources. If you're using AAD, see [Azure Active Directory Authentication Libraries](/azure/active-directory/develop/active-directory-authentication-libraries) for instructions on getting the client ID string.

### Add the SDK

Insert the following repository references into the *build.gradle* file at the root of your project.

```Java
allprojects {
    repositories {
        jcenter()
    }
}
```
Then, insert the following dependency into the _build.gradle_ file that is in your project folder.

```Java
dependencies { 
    ...
    implementation 'com.microsoft.connecteddevices:connecteddevices-sdk:+'
}
```

In your project's *AndroidManifest.xml* file, add the following permissions inside the `<manifest>` element (if they are not already present). This gives your app permission to connect to the Internet and to enable Bluetooth discovery on your device.

Note that the Bluetooth-related permissions are only necessary for using Bluetooth discovery; they are not needed for the other features in the Connected Devices Platform. Additionally, `ACCESS_COARSE_LOCATION` is only required on Android SDKs 21 and later. On Android SDKs 23 and later, the developer must also prompt the user to grant location access at runtime.


```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Next, go to the activity class(es) where you would like the Connected Devices functionality to live. Import the the following packages.

```java
import com.microsoft.connecteddevices;
import com.microsoft.connecteddevices.remotesystems;
import com.microsoft.connecteddevices.remotesystems.commanding;
```