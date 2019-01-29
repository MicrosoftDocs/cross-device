---
title: MCDConnectedDevicesNotificationRegistrationManager
description: Manages the registration for Rome cloud notification for all accounts.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistrationManager` 

```
@interface MCDConnectedDevicesNotificationRegistrationManager : NSObject
```  
Manages the registration for the Connected Devices platform cloud notification for all accounts.

## Properties

### registrationStateChanged
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDConnectedDevicesNotificationRegistrationManager*, MCDConnectedDevicesNotificationRegistrationStateChangedEventArgs*>* registrationStateChanged;`

Event for when the registration state changes for a given account. (from **in_progress** to **succeeded**, for example).

## Methods

### registerForAccountAsync
`- (void) registerForAccountAsync:(MCDConnectedDevicesAccount* _Nonnull) account registration:(MCDConnectedDevicesNotificationRegistration* _Nonnull) notificationRegistration callback:(nonnull void (^)(BOOL, NSError* _Nullable)) callback;`

Register this application for this user with a push notification service so notification can be received by this user.

#### Parameters 
* `account` 

The MCDConnectedDevicesAccount to perform the registration under.

* `notificationRegistration` 

Contains the information required to perform the app's registration with a push notification service.

* `callback` 

The callback result for if the registration completed successfully.

### getNotificationRegistrationStateForAccount
`- (MCDConnectedDevicesNotificationRegistrationState) getNotificationRegistrationStateForAccount:(MCDConnectedDevicesAccount* _Nonnull)account;`

#### Parameters 
* `account`

The MCDConnectedDevicesAccount to get the registration state for.

#### Returns

Return MCDConnectedDevicesNotificationRegistrationState for the registration state.