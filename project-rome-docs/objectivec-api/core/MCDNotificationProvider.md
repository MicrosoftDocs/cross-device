---
title: MCDNotificationProvider
description: This protocol enables an app to become a notification provider to remote apps.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# protocol `MCDNotificationProvider`

```
@protocol MCDNotificationProvider<NSObject>
```

This protocol enables an app to become a notification provider to remote apps.

## Properties 

### registrationUpdated
`@property(nonatomic, readonly, strong, nonnull) MCDRegistrationUpdatedEvent* registrationUpdated;`

An event indicating that the notification registration has changed. When the notification token changes, the app must raise this event.

## Methods

### getNotificationRegistrationAsync
`- (void)getNotificationRegistrationAsync: (nonnull void (^)(MCDNotificationRegistration* _Nullable, NSError* _Nullable))completionBlock;`

This method is called when the MCDPlatform is initialized. The platform queries the app for its notification registration.

#### Parameters
* `completionBlock` The code block to execute upon completion.