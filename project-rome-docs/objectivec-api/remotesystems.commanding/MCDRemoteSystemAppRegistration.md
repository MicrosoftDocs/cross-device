---
title: MCDRemoteSystemAppRegistration
description:  This class represents an application that is to be registered with the Connected Devices platform.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemAppRegistration` 

```
@interface MCDRemoteSystemAppRegistration : NSObject
```  

This class contains all of the information about this app that another could discover and use.

> 
> [!NOTE] MCDRemoteSystemAppRegistration information must be published before any outgoing communication to another app is possble. This is so that the other application can know how to respond to that communication.

## Properties

### account
`@property(nonatomic, readonly, nullable) MCDConnectedDevicesAccount* account;`

Account that this registration belongs to.

### attributes
`@property(nonatomic, copy, nullable) NSDictionary<NSString*, NSString*>* attributes;`

 Dictionary of strings that describe the attributes of this app.

### appServiceProviders
`@property(nonatomic, copy, nullable) NSArray<id<MCDAppServiceProvider>>* appServiceProviders;`

Array of AppServiceProviders that this app supports.

> [!NOTE] 
> An app service provider must be present in this array in order to receive incoming connections.  MCDRemoteSystemAppRegistration.publishAsync() does not need to be called for the app service provider to receive requests.  

### launchUriProvider
`@property(nonatomic, readwrite, nullable) id<MCDLaunchUriProvider> launchUriProvider;`

Launch Uri provider for this app.

> [!NOTE] A launch uri provider must be stored in this property in order to receive incoming requests.  MCDRemoteSystemAppRegistration.publishAsync() does not need to be called for the app service provider to receive requests.  

## Constructors

### getForAccount
`+(nullable instancetype) getForAccount:(MCDConnectedDevicesAccount* _Nonnull) account
                              platform:(MCDConnectedDevicesPlatform* _Nonnull) platform;`

Gets the current remote system app registration for the account.

#### Parameters
* `account` 

Account to retrieve the registration for.

* `platform` 

Platform to get registration from.

#### Returns
Returns an MCDRemoteSystemAppRegistration object for the provided Account.

## Methods

### saveAsync
`- (void)saveAsync:(nonnull void (^)(BOOL, NSError* _Nullable))callback  __attribute__((deprecated("Use publishAsync instead")));`

Saves the information currently stored in the RemoteSystemAppRegistration such that other applications can discover it.

> [!NOTE] MCDConnectedDevicesNotificationRegistration must be registered for this call to succeed.

> [!WARNING] Deprecated. Use publishAsync instead.

#### Parameters

* `callback`

The callback indicates the result of saving the information.

### publishAsync
`- (void)publishAsync:(nonnull void (^)(MCDRemoteSystemAppRegistrationPublishResult* _Nonnull, NSError* _Nullable))completionBlock;`

Publishes the information currently stored in the MCDRemoteSystemAppRegistration such that other applications can discover it.

> [!NOTE] MCDConnectedDevicesNotificationRegistration must be registered for this call to succeed.

#### Parameters

* `callback`

The callback indicates the result of saving the information.