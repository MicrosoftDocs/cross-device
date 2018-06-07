---
title: MCDApplicationRegistrationBuilder
description: A builder class for MCDApplicationRegistration instances.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDApplicationRegistrationBuilder`

```
@interface MCDApplicationRegistrationBuilder : NSObject
```

A builder class for MCDApplicationRegistration instances.

## Methods

### addAttribute
`- (void)addAttribute:(NSString*)value forName : (NSString*)name;`

Add a key/value attribute to the application registration. For example, your app could define a unique ID attribute and share it with client devices. Then they can look for it in subsequent discoveries.

You can change your app's registered attributes by rebuilding an **ApplicationRegistration** with new attributes and re-initializing the Connected Devices Platform, but it is recommended that you keep your attributes constant, possibly adding more as needed when you update your app.

#### Parameters
* `value` The attribute value.
* `name` The name of the attribute.

### addAppServiceProvider
`- (void)addAppServiceProvider:(id<MCDAppServiceProvider>)provider;`

Add an app service provider to the application registration.

#### Parameters
* `provider` The app service provider to add.

### setLaunchUriProvider
`- (void)setLaunchUriProvider:(id<MCDLaunchUriProvider>)provider;`

Set the launch URI provider for the application registration.

#### Parameters
* `provider` The URI provider to add.

### buildRegistration
`- (MCDApplicationRegistration*)buildRegistration;`

Builds an application registration with the specified properties.

#### Returns
A new MCDApplicationRegistration instance.

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


