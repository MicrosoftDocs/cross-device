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

## Initialize the Connected Devices platform

Before any Connected Devices features can be used, the platform must be initialized within your app. 

You must instantiate the **MCDPlatform** class. The **MCDPlatform**'s `platformWithAccountProvider:` method takes two parameters: a **MCDUserAccountProvider** and a **MCDNotificationProvider**. The **MCDNotificationProvider** parameter is only needed for remote app hosting and User Activities, which are not covered in this guide. It can be left `nil` for now.

The **MCDUserAccountProvider** is needed to deliver an OAuth 2.0 access token for the current user's access to the Connected Devices Platform. It will be called the first time the app is run and upon the expiration of a platform-managed refresh token. 

In order to help developers onboard with the platform more easily, we have provided account provider implementations for Android and iOS. These implementations, found in the [authentication provider sample](https://github.com/Microsoft/project-rome/tree/master/iOS/samples/account-provider-sample), can be used to obtain the OAuth 2.0 access token and refresh token for your app.

[!INCLUDE [auth-scopes](../auth-scopes.md)]

The following code from the sample app shows the initialization of the platform.

```ObjectiveC
- (void)initializePlatform
{
    // Only register for APNs if this app is enabled for push notifications
    NotificationProvider* notificationProvider;
    if ([[UIApplication sharedApplication] isRegisteredForRemoteNotifications])
    {
        notificationProvider = [AppDataSource sharedInstance].notificationProvider;
    }
    else
    {
        NSLog(@"Initializing platform without a notification provider!");
        notificationProvider = nil;
    }

    // Initialize platform
    [AppDataSource sharedInstance].platform = [MCDPlatform platformWithAccountProvider:[AppDataSource sharedInstance].accountProvider notificationProvider:notificationProvider];

    // ...
}
```

You should shut down the platform when your app exits the foreground by calling the `shutdownAsync:` method.
