---
title: MCDConnectedDevicesPlatform
description: TODO
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesPlatform` 

```
@interface MCDConnectedDevicesPlatform : NSObject
```  
TODO

## Properties

### accountManager
`@property (nonatomic, readonly, nonnull) MCDConnectedDevicesAccountManager* accountManager;`

TODO

### notificationRegistrationManager
`@property (nonatomic, readonly, nonnull) MCDConnectedDevicesNotificationRegistrationManager* notificationRegistrationManager;`

TODO

## Constructors

### platformWithSettings
`+ (nullable instancetype)platformWithSettings:(MCDConnectedDevicesPlatformSettings* _Nonnull)settings;`

TODO

#### Parameters 
* `settings` 

TODO

#### Returns
TODO

### processNotification
`- (MCDConnectedDevicesProcessNotificationOperation* _Nonnull)processNotification:(NSString* _Nonnull)notification;`

TODO

#### Parameters 
* `notification` 

TODO

## Methods

### start
`- (void) start;`

TODO

### shutdownAsync
`- (void)shutdownAsync:(void (^_Nonnull)(NSError* _Nullable))completionBlock;`

TODO

#### Parameters 
* `completionBlock` 

TODO

### processNotification
`- (MCDConnectedDevicesProcessNotificationOperation* _Nonnull)processNotification:(NSString* _Nonnull)notification;`

TODO

#### Parameters 
* `notification` 

TODO

#### Returns
TODO