---
title: MCDConnectedDevicesNotificationRegistrationStateChangedEventArgs
description: Event Args class for the MCDConnectedDevicesNotificationRegistration State Changed event.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistrationStateChangedEventArgs` 

```
@interface MCDConnectedDevicesNotificationRegistrationStateChangedEventArgs : NSObject
```  
Event Args class for the MCDConnectedDevicesNotificationRegistration State Changed event. This is used to ensure that the application gets informed about new Connected Devices platform messages via the correct notification mechanism.

## Properties

### account
`@property(nonatomic, readonly, nonnull) MCDConnectedDevicesAccount* account;`

The Account for which the notification registration state has changed for.

### registration
`@property(nonatomic, readonly, nonnull) MCDConnectedDevicesNotificationRegistration* registration;`

The information for registration instance whose state has changed.

### state
`@property(nonatomic, readonly) MCDConnectedDevicesNotificationRegistrationState state;`

The new registration state.