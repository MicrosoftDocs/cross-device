---
title: MCDRemoteSystemApplicationRegistration
description: This class represents an application that is registered for remote connectivity.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDRemoteSystemApplicationRegistration`

```
@interface MCDRemoteSystemApplicationRegistration : NSObject 
```

This class represents an application that is registered for remote connectivity. It can provide remote app services or be used to launch a URI.

## Properties

### attributes 
`@property(nonatomic, readonly, nullable) NSDictionary<NSString*, NSString*>* attributes;`

A dictionary of key/value pairs defining the attributes of this registration. For example, your app could define a unique ID attribute and share it with client devices. Then they can look for it in subsequent discoveries.

## Methods
### addCloudRegistrationStatusChangedListener
`- (NSUInteger)addCloudRegistrationStatusChangedListener:(nonnull void (^)(MCDUserAccount* _Nonnull, MCDCloudRegistrationStatus))listener;`

Adds an event listener for the "Cloud registration status changed" event, which is raised when the status of this registration changes (from **MCDCloudRegistrationStatusInProgress** to **MCDCloudRegistrationStatusSucceeded**, for example).

#### Parameters
* `listener` The event listener to handle this event.

#### Returns
The event registration token (needed to unregister this listener).

### removeCloudRegistrationStatusChangedListener
`- (void)removeCloudRegistrationStatusChangedListener:(NSUInteger)eventRegistrationToken;`

Removes a previously-registered event listener from the "Cloud registration status changed" event.

#### Parameters
* `eventRegistrationToken` The unique identifier for the event registration that is to be undone.

### start
`- (void)start;`

Starts the process of registering this application in the cloud.


## Example

The following sample code shows how to use an MCDRemoteSystemApplicationRegistration instance to register your app with the cloud.

```ObjectiveC
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
```


