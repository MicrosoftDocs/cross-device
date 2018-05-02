---
title: MCDPlatform
description:  A static class to perform global scale commands to the Connected Devices Platform.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDPlatform` 

```
@interface MCDPlatform : NSObject 
```  

A static class to perform global scale commands to the Connected Devices Platform.

## Methods

### createWithNotificationProviderAsync
`+ (void)createWithNotificationProviderAsync:(id _Nullable)notificationProvider
                    applicationRegistration:(id _Nullable)applicationRegistration
                            accountProvider:(id<MCDUserAccountProvider> _Nonnull)accountProvider
                                 completion:(void (^_Nonnull)(MCDPlatformCreationResult* _Nonnull, NSError* _Nullable))completionBlock;`

Initializes the Remote Systems Platform. This must be invoked before attempting to use any Remote Systems functionality.

#### Parameters
* `notificationProvider` The id of the notification provider for this platform instance.
* `applicationRegistration` The id of the application registration for this platform instance.
* `accountProvider` The id of the user account provider for this platform instance.
* `completionBlock` The block to invoke upon completion. This handles the [MCDPlatformCreationResult](MCDPlatformCreationResult.md), which contains an MCDPlatform instance as a property.

### shutdownAsync
`- (void)shutdownAsync:(void (^_Nonnull)(NSError* _Nullable))completionBlock;`

Shuts down the Remote Systems Platform.

#### Parameters
* `completionBlock` The block to invoke upon completion.

## Example

The following sample code shows the initialization of MCDPlatform.

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
