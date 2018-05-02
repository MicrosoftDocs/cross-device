---
title: MCDApplicationRegistration
description: This class represents an application that is registered for remote connectivity.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDApplicationRegistration`

```
@interface MCDApplicationRegistration : NSObject
```

This class represents an application that is registered for remote connectivity. It can provide remote app services or be used to launch a URI.

## Properties

### attributes 
`@property(nonatomic, readonly, nullable) NSDictionary<NSString*, NSString*>* attributes;`

A dictionary of key/value pairs defining the attributes of this registration.

### appServiceProviders
`@property(nonatomic, readonly, nullable) NSArray<id<MCDAppServiceProvider>>* appServiceProviders;`

An array of app services available for this application.

### launchUriProvider
`@property(nonatomic, readonly, nullable) id<MCDLaunchUriProvider> launchUriProvider;`

The URI launcher for this application.

## Example

The following sample code shows the initialization of MCDPlatform, using an MCDApplicationRegistration instance.

```Objective-C
-(void)initializePlatform {
    
    // Rome is initialized asynchronously
    dispatch_async(dispatch_get_global_queue( DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        MCDApplicationRegistrationBuilder* builder = [MCDApplicationRegistrationBuilder new];
        MCDApplicationRegistration* registration = [builder buildRegistration];
        
        // notifications are optional - not covered here.
        NotificationProvider* notificationProvider = nil;
        
        // Initialize platform
        [MCDPlatform createWithNotificationProviderAsync:notificationProvider
                                 applicationRegistration:registration
                                         accountProvider:[IdentityViewController accountProvider]
                                              completion:^(MCDPlatformCreationResult* result, __unused NSError* error) {
                                                  NSLog(@"Initialized platform callback");
                                              }];
        // Now the platform is initialized it's safe to enable button
        [self.deviceRelayButton setEnabled:YES];
        [self.activityFeedButton setEnabled:YES];
    });
}
```


