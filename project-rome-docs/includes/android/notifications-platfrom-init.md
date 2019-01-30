---
title: include file
description: include file
ms.topic: include
ms.assetid: 9f679e13-b1b3-40f8-bd44-679e4dffc0d4
ms.localizationpriority: medium
---

### Add the SDK

Insert the following repository references into the *build.gradle* file at the root of your project.

```java
allprojects {
    repositories {
        jcenter()
        maven { url 'https://maven.google.com' }
        maven { url 'https://projectrome.bintray.com/maven/' }
    }
}
```
Then, insert the following dependency into the _build.gradle_ file that is in your project folder.

```java
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

Next, go to the activity class(es) where you would like to add the Connected Devices functionality. Import the **connecteddevices** namespaces.

```java
import com.microsoft.connecteddevices.*;
```

Depending on which scenarios you implement, you many not need all of the namespaces. You may also need to add other Android-native namespaces as you progress.

### Initialize the Connected Devices Platform

Before any Connected Devices features can be used, the platform must be initialized within your app. The initialization steps should occur in your main class' **onCreate** or **onResume** method, because they are required before other Connected Devices scenarios can take place. 

You must instantiate the **Platform** class. The **Platform** constructor takes three parameters: the **Context** for the app, a **NotificationProvider**, and a **UserAccountProvider**.

The **NotificationProvider** parameter is only needed for certain scenarios. In the case of using Microsoft Graph Notifications, it is required. Leave it as `null` for now and find out how to enable the client SDK to handle incoming user-centric notifications via native push channels in next section.

The **UserAccountProvider** is needed to deliver an OAuth 2.0 access token for the current user's access to the Connected Devices Platform. It will be called the first time the app is run and upon the expiration of a platform-managed refresh token. 

In order to help developers onboard with the platform more easily, we have provided account provider implementations for Android and iOS. These implementations, found in the [authentication provider sample](https://github.com/Microsoft/project-rome/tree/master/Android/samples/account-provider-sample), can be used to obtain the OAuth 2.0 access token and refresh token for your app.

[!INCLUDE [auth-scopes](../auth-scopes.md)]

In the code below, `mSignInHelper` references an **MSAAccountProvider**, also initialized below. This provided class implements the **UserAccountProvider** interface.

```java
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

```java
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
In your main class, where `mSignInHelper` is initialized, add the following code.

```java
private Platform mPlatform;

//...

mPlatform = PlatformHelperClass.getOrCreatePlatform(this, mSignInHelper, null);
```

You should shut down the platform when your app exits the foreground.

```Java
mPlatform.shutdownAsync();
```
