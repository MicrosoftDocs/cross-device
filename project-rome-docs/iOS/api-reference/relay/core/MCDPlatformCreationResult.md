---
title: MCDPlatformCreationResult
description:  This class is the result of an attempt to initialize an MCDPlatform.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDPlatformCreationResult` 

```
@interface MCDPlatformCreationResult : NSObject
```  

This class is the result of an attempt to initialize an MCDPlatform.

## Properties

### status
`@property(nonatomic, readonly) MCDPlatformCreationStatus status;`

The status of the Platform initialization attempt.

### platform
`@property(nonatomic, readonly, nullable) MCDPlatform* platform;`

The initialized MCDPlatform instance, if the attempt was successful.


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
