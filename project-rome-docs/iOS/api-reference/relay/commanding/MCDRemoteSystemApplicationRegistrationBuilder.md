---
title: MCDRemoteSystemApplicationRegistrationBuilder
description: A builder class for MCDRemoteSystemApplicationRegistration instances.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDRemoteSystemApplicationRegistrationBuilder`

```
@interface MCDRemoteSystemApplicationRegistrationBuilder : NSObject 
```

A builder class for MCDRemoteSystemApplicationRegistration instances.

## Methods

### addAttribute
`- (void)addAttribute:(NSString*)value forName : (NSString*)name;`

Add a key/value attribute to the application registration. For example, your app could define a unique ID attribute and share it with client devices. Then they can look for it in subsequent discoveries.

You can change your app's registered attributes by rebuilding an **ApplicationRegistration** with new attributes and re-initializing the Connected Devices Platform, but it is recommended that you keep your attributes constant, possibly adding more as needed when you update your app.

#### Parameters
* `value` The attribute value.
* `name` The name of the attribute.

### buildRegistration
`- (MCDRemoteSystemApplicationRegistration*)buildRegistration;`

Builds an application registration with the specified properties.

#### Returns
A new MCDRemoteSystemApplicationRegistrationBuilder instance.

## Example

The following sample code shows how to use an MCDRemoteSystemApplicationRegistration instance to register your app with the cloud (first using an MCDHostingRemoteSystemApplicationRegistrationBuilder to build the instance).

```ObjectiveC
// App is registered asynchronously.
c* builder = [MCDHostingRemoteSystemApplicationRegistrationBuilder new];
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
```