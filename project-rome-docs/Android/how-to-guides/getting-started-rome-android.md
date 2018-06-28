---
title: Getting started with Connected Devices (Android)
description: This guide shows you how to set up the Connected Devices Platform on an Android app and use it to discover and connect to remote devices and apps.
keywords: microsoft, windows, project rome, Android api reference 
---

# Getting started with Connected Devices (Android)
This guide shows you how to set up the Connected Devices Platform on an Android app and use it to discover and connect to remote devices and apps. Refer to the [Android sample app](https://github.com/Microsoft/project-rome/tree/master/Android/samples) for a working example of all Android scenarios.


## Preliminary setup for Connected Devices functionality

Before implementing remote connectivity, there are a few steps you'll need to take to give your Android app the capability to connect to remote Windows devices.

### Sign-in

Microsoft Account (MSA) authentication is required for all features of the SDK, other than the Nearby Sharing APIs. 

If you do not already have an MSA, Register for one on [account.microsoft.com](https://account.microsoft.com/account).

The Project Rome SDK requires an OAuth 2.0 access token to register with the platform. An OAuth 2.0 access token can be obtained using the developer's preferred method. In an attempt to help developers onboard with the platform more easily, we have provided an authentication provider as part of the  
Android and iOS samples. The [sample authentication provider](https://github.com/Microsoft/project-rome/tree/master/Android/samples/account-provider-sample) can be used to obtain the OAuth 2.0 access token and refresh token for your app.

Next, you must register your app with Microsoft by following the cross platform instructions on the [Application Registration Portal](https://apps.dev.microsoft.com/) (if you do not have a Microsoft developer account created, you must do this first). You should receive a client ID string for your app - save this for later. This will allow your app to access Microsoft's Connected Devices Platform resources. 

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

> **Note:** The Bluetooth-related permissions are only necessary for using Bluetooth discovery; they are not needed for the other features in the Connected Devices platform. Additionally, `ACCESS_COARSE_LOCATION` is only required on Android SDKs 21 and later. On Android SDKs 23 and later, the developer must also prompt the user to grant location access at runtime.

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Next, go to the activity class(es) where you would like the Connected Devices functionality to live. Add the **connecteddevices** namespaces.

```java
import com.microsoft.connecteddevices.*;
```

Depending on which scenarios you implement, you many not need all namespaces. You may also need to add other Android-native namespaces as you progress.


## Initialize the Connected Devices platform

Before any Connected Devices features can be used, the platform must be initialized. 

The **Platform** class' constructor takes three parameters: the **Context** for the app, a **NotificationProvider**, and a **UserAccountProvider**. This section shows how to get these parameters. These initialization steps should occur in your main class' **onCreate** or **onResume** method, because they are required before other Connected Devices scenarios can take place. 

The **NotificationProvider** parameter is only needed for remote app hosting and User Activities, which are not covered in this guide. It can be left `null` for the scenarios here.

The **UserAccountProvider** is needed to deliver an ID for the current user to the Connected Devices Platform. It will be called the first time the app is run and upon the expiration of a platform-managed refresh token. This is where the class(es) in the [sample authentication provider](https://github.com/Microsoft/project-rome/tree/master/Android/samples/account-provider-sample) can be used. In the code below, `getSignInHelper()` references an **MSAAccountProvider**, also initialized below; this provided class implements the **UserAccountProvider** interface, and it facilitates the account-fetching process.

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

Then, construct a **Platform** instance. You may wish to put the following code in a separate helper class. 

```Java
// Platform helper class:

private static Platform sPlatform;

//...

// This is the main Platform-generating method
public static synchronized Platform getOrCreatePlatform(Context context, UserAccountProvider accountProvider, NotificationProvider notificationProvider) {
    Platform platform = getPlatform();

    if (platform == null) {
        platform = createPlatform(context, accountProvider, notificationProvider);
    }
    return platform;
}

public static synchronized Platform getPlatform() {
        return sPlatform;
}

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

> **Important:** As this is a preview release, there are some known bugs in the Project Rome platform. Currently, shutting down the Connected Devices Platform will cause the app to crash. This is trivial if it is only done when the app is exiting, but we are working on a timely fix. 

Next, you must register the application with the Connected Devices Platform cloud directory. You may wish to put the following method in a separate helper class.

```Java

public static void register(Context context, ArrayList<AppServiceProvider> appServiceProviders, LaunchUriProvider launchUriProvider, EventListener<UserAccount, CloudRegistrationStatus> listener) {
    
    // initialize the ApplicationRegistration with all possible services
    RemoteSystemApplicationRegistrationBuilder builder = new RemoteSystemApplicationRegistrationBuilder();
    builder.addAttribute("SampleAttribute", "Value");

    // Add the given AppService and LaunchUri Providers to the registration builder
    if (appServiceProviders != null) {
        for (AppServiceProvider provider : appServiceProviders) {
            builder.addAppServiceProvider(provider);
        }
    }
    if (launchUriProvider != null) {
        builder.setLaunchUriProvider(launchUriProvider);
    }

    // Build the ApplicationRegistration instance
    IRemoteSystemApplicationRegistration registration = builder.buildRegistration();

    // Add the given EventListener to handle registration completion
    registration.addCloudRegistrationStatusChangedListener(listener);
    // start cloud registration
    registration.start();
}
```

In your main class, after **Platform** initialization, add the following code to register the application. Note that for the purpose of this simple example, app service providers and launch URI handler are not provided.

```Java
RegistrationHelperClass.register(this, null, null, new EventListener<UserAccount, CloudRegistrationStatus>() {
    // define an event listener to handle the cloud registration operation:
    @Override
    public void onEvent(UserAccount account, CloudRegistrationStatus status) {
        switch (status) {
            case NOT_STARTED:
                Log.d(TAG, "Registration has not started.");
                break;
            case IN_PROGRESS:
                Log.d(TAG, "Registration in progress...");
                break;
            case SUCCEEDED:
                Log.d(TAG, "Completed Rome registration");
                // do other work now that registration has succeeded
                break;
            case FAILED:
                Log.d(TAG, "Rome registration failed!");
                break;
        }
    }
});
```

At this point, your next actions will depend on which scenario(s) you intend to implement. For Device Relay scenarios, such as launching an app on a remote device or communicating with an app service on a remote device, see the [Command remote devices and apps](command-remote-devices-and-apps-android.md) guide (this also covers nearby sharing with other devices). For User Activities scenarios, such as creating, publishing, and reading Windows user activities, see the [Publish and read user activities](user-activities-android.md) guide. To make your app a host (able to be remotely launched or deliver app service resources to a remote device), see the [Host cross-device experiences](hosting-android.md) guide.
