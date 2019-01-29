---
title: MCDRemoteSystemAppRegistration
description:  This class represents an application that is to be registered with the Connected Devices platform.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemAppRegistration` 

```
@interface MCDRemoteSystemAppRegistration : NSObject
```  

This class represents an application that is to be registered with the Connected Devices platform.
Registration is required (**saveAsync** must have successfully completed) to receive responses from commands as well as to allow other apps to discover this application and its attributes and capabilities.

## Properties

### account
`@property(nonatomic, readonly, nullable) MCDConnectedDevicesAccount* account;`

The current MCDConnectedDevicesAccount account provided.

### attributes
`@property(nonatomic, copy, nullable) NSDictionary<NSString*, NSString*>* attributes;`

A **Map** of attributes to set in the registration.

### appServiceProviders
`@property(nonatomic, copy, nullable) NSArray<id<MCDAppServiceProvider>>* appServiceProviders;`

The app service providers associated with the registration. New values are made available to discovering apps and devices via the **saveAsync** call.

### launchUriProvider
`@property(nonatomic, readwrite, nullable) id<MCDLaunchUriProvider> launchUriProvider;`

The launch uri provider associated with this application.

## Constructors

### getForAccount
`+(nullable instancetype) getForAccount:(MCDConnectedDevicesAccount* _Nonnull) account
                              platform:(MCDConnectedDevicesPlatform* _Nonnull) platform;`

Creates and initializes a new instance of this class.

#### Parameters
* `account` 

The current MCDConnectedDevicesAccount account provided.

* `platform` 

The current MCDConnectedDevicesPlatform account provided.

#### Returns
Returns an MCDRemoteSystemAppRegistration object for the provided Account.

## Methods

### saveAsync
`- (void)saveAsync:(nonnull void (^)(BOOL, NSError* _Nullable))callback;`

Saves the registration so that other apps and devices can discover it.

#### Parameters

* `callback`

The callback result indicates if the registration was saved or not. 