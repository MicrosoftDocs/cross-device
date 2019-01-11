---
title: MCDConnectedDevicesNotificationRegistrationManager
description: TODO
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistrationManager` 

```
@interface MCDConnectedDevicesNotificationRegistrationManager : NSObject
```  
TODO

## Properties

### registrationStateChanged
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDConnectedDevicesNotificationRegistrationManager*, MCDConnectedDevicesNotificationRegistrationStateChangedEventArgs*>* registrationStateChanged;`

TODO

## Methods

### registerForAccountAsync
`- (void) registerForAccountAsync:(MCDConnectedDevicesAccount* _Nonnull) account registration:(MCDConnectedDevicesNotificationRegistration* _Nonnull) notificationRegistration callback:(nonnull void (^)(BOOL, NSError* _Nullable)) callback;`

TODO

#### Parameters 
* `notificationRegistration callback` 

TODO

* `callback` 

TODO

### getNotificationRegistrationStateForAccount
`- (MCDConnectedDevicesNotificationRegistrationState) getNotificationRegistrationStateForAccount:(MCDConnectedDevicesAccount* _Nonnull)account;`

TODO

#### Parameters 
* `account` TODO

#### Returns
TODO