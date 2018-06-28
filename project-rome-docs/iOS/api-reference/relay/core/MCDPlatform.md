---
title: MCDPlatform
description:  A class to represent the Connected Devices Platform and manage the app's connection to it.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDPlatform` 

```
@interface MCDPlatform : NSObject 
```  

A class to represent the Connected Devices Platform and manage the app's connection to it.

## Constructors

### platformWithAccountProvider
`+ (nullable instancetype)platformWithAccountProvider:(id<MCDUserAccountProvider> _Nullable)accountProvider
                               notificationProvider:(id _Nullable)notificationProvider;`

Creates and initializes a new instance of this class.

#### Parameters

* `accountProvider` The user account provider for this platform instance.
* `notificationProvider` The id of the notification provider for this platform instance.

### shutdownAsync
`- (void)shutdownAsync:(void (^_Nonnull)(NSError* _Nullable))completionBlock;`

Shuts down the Remote Systems Platform.

#### Parameters
* `completionBlock` The block to invoke upon completion.

## Example

The following sample code shows the initialization of MCDPlatform.

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

    // App is registered asynchronously.
    MCDHostingRemoteSystemApplicationRegistrationBuilder* builder = [MCDHostingRemoteSystemApplicationRegistrationBuilder new];
    [builder setLaunchUriProvider:[[LaunchUriProvider alloc] initWithDelegate:[AppDataSource sharedInstance].inboundRequestLogger]];
    [builder addAppServiceProvider:[[AppServiceProvider alloc] initWithDelegate:[AppDataSource sharedInstance].inboundRequestLogger]];
    [builder addAttribute:@"ExampleAttribute" forName:@"ExampleName"];
    MCDRemoteSystemApplicationRegistration* registration = [builder buildRegistration];
    
    [registration addCloudRegistrationStatusChangedListener:^(MCDUserAccount * _Nonnull account, MCDCloudRegistrationStatus status) {
        NSLog(@"Cloud Registration Status Changed listener");
        switch (status) {
            case MCDCloudRegistrationStatusFailed:
                NSLog(@"Cloud registration completed with status Failed");
                break;
            case MCDCloudRegistrationStatusInProgress:
                NSLog(@"Cloud registration in progress");
                break;
            case MCDCloudRegistrationStatusNotStarted:
                NSLog(@"Cloud registration not started");
                break;
            case MCDCloudRegistrationStatusSucceeded:
                dispatch_async(dispatch_get_main_queue(), ^{
                    // The app has been registered.  It is safe to enable button.
                    [self.deviceRelayButton setEnabled:YES];
                    [self.activityFeedButton setEnabled:YES];
                });
                break;
        }
    }];
    
    [registration start];
}
```