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

MCDConnectedDevicesNotificationRegistrationManager manages the notification information registered for each account. Any time an app's notification information changes (for example, when APNS changes its token), or when the notification information is expiring, an app should re-register its information. 
If an application only cares about responses to outgoing communication, a Polling registration may be used.

> [!NOTE] 
> Notification information must be registered before many ConnectedDevices scenarios will work successfully. 

## Properties

### registrationStateChanged
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDConnectedDevicesNotificationRegistrationManager*, MCDConnectedDevicesNotificationRegistrationStateChangedEventArgs*>* registrationStateChanged;`

Event to let the app know when notification registration state changes for an account. 

## Methods

### registerForAccountAsync
`- (void) registerForAccountAsync:(MCDConnectedDevicesAccount* _Nonnull)account registration:(MCDConnectedDevicesNotificationRegistration* _Nonnull)notificationRegistration callback:(nonnull void (^)(BOOL, NSError* _Nullable))callback __attribute__((deprecated("Use registerAsync instead")));`

Register the given account with the given notification registration information. This creates a notification channel so that this application can be notified about new Connected Devices information for this account. Note that other applications can not communicate with this app using this notification channel until 
the MCDRemoteSystemAppRegistration information is published.

> [!WARNING]
> This funciton is deprecated. Please use registerAsync instead.

#### Parameters 
* `account` 

Account for which to register notification information.

* `notificationRegistration` 

Notification information to register.

* `callback` 

The callback result for if the registration completed successfully.

### registerAsync
`- (void) registerAsync:(MCDConnectedDevicesAccount* _Nonnull)account registration:(MCDConnectedDevicesNotificationRegistration* _Nonnull)notificationRegistration completion:(nonnull void (^)(MCDConnectedDevicesNotificationRegistrationResult* _Nonnull, NSError* _Nullable))callback;`

Register the given account with the given notification registration information. This creates a notification channel so that this application can be notified about new Connected Devices information for this account. Note that other applications can not communicate with this app using this notification channel until the MCDRemoteSystemAppRegistration information is published.

#### Parameters 
* `account` 

Account for which to register notification information.

* `notificationRegistration` 

Notification information to register.

* `callback` 

The callback result for if the registration completed successfully.

### getNotificationRegistrationStateForAccount
`- (MCDConnectedDevicesNotificationRegistrationState) getNotificationRegistrationStateForAccount:(MCDConnectedDevicesAccount* _Nonnull)account;`

Retrieve the current notification registration state for the given account. The notification information that is registered will eventually expire (useful if the app is uninstalled or not run in a very long time). An app should re-register its notificaiton information when the registration is expiring / expired. 

#### Parameters 
* `account`

Account for which to get registration state.

#### Returns

State of the notification registration.
