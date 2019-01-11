---
title: MCDRemoteSystemAppRegistration
description:  TODO
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemAppRegistration` 

```
@interface MCDRemoteSystemAppRegistration : NSObject
```  

TODO

## Properties

### account
`@property(nonatomic, readonly, nullable) MCDConnectedDevicesAccount* account;`

TODO

### attributes
`@property(nonatomic, copy, nullable) NSDictionary<NSString*, NSString*>* attributes;`

TODO

### appServiceProviders
`@property(nonatomic, copy, nullable) NSArray<id<MCDAppServiceProvider>>* appServiceProviders;`

TODO

### launchUriProvider
`@property(nonatomic, readwrite, nullable) id<MCDLaunchUriProvider> launchUriProvider;`

TODO


## Constructors

### getForAccount
`+(nullable instancetype) getForAccount:(MCDConnectedDevicesAccount* _Nonnull) account
                              platform:(MCDConnectedDevicesPlatform* _Nonnull) platform;`

#### Parameters
* `account` TODO
* `platform` TODO

#### Returns
The initialized TODO

## Methods

### saveAsync
`- (void)saveAsync:(nonnull void (^)(BOOL, NSError* _Nullable))callback;`

TODO

#### Parameters

### callback
TODO