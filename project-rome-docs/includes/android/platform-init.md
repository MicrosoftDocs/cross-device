---
title: include file
description: include file
ms.author: pafarley
ms.date: 07/17/2018
ms.topic: include
ms.prod: windows
ms.technology: uwp
ms.assetid: 3bee862f-1fbf-4f42-9dbf-e8ee79cb3831
ms.localizationpriority: medium
---

## Preliminary setup for the Connected Devices Platform

Before implementing remote connectivity, there are a few steps you'll need to take to give your Android app the capability to connect to remote devices.

### Sign-in

Microsoft Account (MSA) or Azure Active Directory (AAD) authentication is required for all features of the SDK, except for the Nearby sharing APIs. 

If you do not already have an MSA and wish to use one, register on [account.microsoft.com](https://account.microsoft.com/account).

Next, you must register your app with Microsoft by following the cross platform instructions on the [Application Registration Portal](https://apps.dev.microsoft.com/) (if you do not have a Microsoft developer account, you must create one first). You should receive a client ID string for your app; save this for later. This will allow your app to access Microsoft's Connected Devices Platform resources. 

### Add the SDK

Insert the following repository references into the *build.gradle* file at the root of your project.

```Java
allprojects {
    repositories {
        jcenter()
        maven { url 'https://maven.google.com' }
        maven { url 'https://projectrome.bintray.com/maven/' }
    }
}
```
Then, insert the following dependency into the _build.gradle_ file that is in your project folder.

```Java
dependencies { 
    ...
    implementation 'com.microsoft.connecteddevices:connecteddevices-sdk:0.11.0'
}
```

If you wish to use ProGuard in your app, add the ProGuard Rules for these new APIs. Create a file called *proguard-rules.txt* in the *App* folder of your project, and paste in the contents of [ProGuard_Rules_for_Android_Rome_SDK.txt](https://github.com/Microsoft/project-rome/blob/master/Android/ProGuard_Rules_for_Android_Rome_SDK.txt).

In your project's *AndroidManifest.xml* file, add the following permissions inside the `<manifest>` element (if they are not already present). This gives your app permission to connect to the Internet and to enable Bluetooth discovery on your device.

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

> [!NOTE]
> The Bluetooth-related permissions are only necessary for using Bluetooth discovery; they are not needed for the other features in the Connected Devices Platform. Additionally, `ACCESS_COARSE_LOCATION` is only required on Android SDKs 21 and later. On Android SDKs 23 and later, the developer must also prompt the user to grant location access at runtime.

Next, go to the activity class(es) where you would like the Connected Devices functionality to live. Import the **connecteddevices** namespaces.

```java
import com.microsoft.connecteddevices.*;
```

Depending on which scenarios you implement, you many not need all of the namespaces. You may also need to add other Android-native namespaces as you progress.

### Initialize the Connected Devices Platform

Before any Connected Devices features can be used, the platform must be initialized within your app. The initialization steps should occur in your main class' **onCreate** or **onResume** method, because they are required before other Connected Devices scenarios can take place. 

You must instantiate the **Platform** class. The **Platform** constructor takes three parameters: the **Context** for the app, a **NotificationProvider**, and a **UserAccountProvider**.

The **NotificationProvider** parameter is only needed for certain scenarios. It can be left `null` for now.

The **UserAccountProvider** is needed to deliver an OAuth 2.0 access token for the current user's access to the Connected Devices Platform. It will be called the first time the app is run and upon the expiration of a platform-managed refresh token. 

In order to help developers onboard with the platform more easily, we have provided account provider implementations for Android and iOS. These implementations, found in the [authentication provider sample](https://github.com/Microsoft/project-rome/tree/master/Android/samples/account-provider-sample), can be used to obtain the OAuth 2.0 access token and refresh token for your app.

In the code below, `getSignInHelper()` references an **MSAAccountProvider**, also initialized below; this provided class implements the **UserAccountProvider** interface, and it facilitates the account-fetching process.

```Java
private MSAAccountProvider mSignInHelper;

// ...

// Create sign-in helper from helper lib, which does user account and access token management for us
// Takes two parameters: a client id for msa, and the Context
mSignInHelper = new MSAAccountProvider(Secrets.MSA_CLIENT_ID, getContext());

// add an event listener, which changes the button text when account state changes
mSignInHelper.addUserAccountChangedListener(new EventListener<UserAccountProvider, Void>() {
    @Override
    public void onEvent(UserAccountProvider provider, Void aVoid){
        if (mSignInHelper.isSignedIn()) {
            // update the UI indicating a user is signed in.
        }
        else
        {
            // update the UI indicating a user is not signed in.
        }
    }
});
```

Now you can construct a **Platform** instance. You may wish to put the following code in a separate helper class. 

```Java
// Platform helper class:

private static Platform sPlatform;

//...

// This is the main Platform-generating method
public static synchronized Platform getOrCreatePlatform(Context context, UserAccountProvider accountProvider, NotificationProvider notificationProvider) {
    // check whether the local platform variable is already initialized.
    Platform platform = getPlatform();

    if (platform == null) {
        // if it is not initialized, do so:
        platform = createPlatform(context, accountProvider, notificationProvider);
    }
    return platform;
}

// gets the local platform variable
public static synchronized Platform getPlatform() {
        return sPlatform;
}

// creates and returns a new Platform instance
public static synchronized Platform createPlatform(Context context, UserAccountProvider accountProvider, NotificationProvider notificationProvider) {
    sPlatform = new Platform(context, accountProvider, notificationProvider);
    return sPlatform;
}

```
Then in your main class, in which you initialized `mSignInHelper`, fill in the following code.

```Java
private Platform mPlatform;

//...

mPlatform = PlatformHelperClass.getOrCreatePlatform(this, mSignInHelper, null);
```

You should shut down the platform when your app exits the foreground.

```Java
mPlatform.shutdownAsync();
```

> [!IMPORTANT] 
> As this is a preview release, there are some known bugs in the Project Rome platform. Currently, shutting down the Connected Devices Platform will cause the app to crash. This is trivial if it is only done when the app is exiting, but we are working on a timely fix. 

