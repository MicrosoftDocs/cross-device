---
title: MCDConnectedDevicesPlatform
description: A class to represent the Connected Devices Platform and manage the app's connection to it.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesPlatform` 

```
@interface MCDConnectedDevicesPlatform : NSObject
```  
This class to represent the Connected Devices Platform and manage the app's connection to it.

## Properties

### accountManager
`@property (nonatomic, readonly, nonnull) MCDConnectedDevicesAccountManager* accountManager;`

MCDConnectedDevicesAccountManager instance held by the platform.

### notificationRegistrationManager
`@property (nonatomic, readonly, nonnull) MCDConnectedDevicesNotificationRegistrationManager* notificationRegistrationManager;`

MCDConnectedDevicesNotificationRegistrationManager instance held by platform.

## Constructors

### platformWithSettings
`+ (nullable instancetype)platformWithSettings:(MCDConnectedDevicesPlatformSettings* _Nonnull)settings;`

A new instance of this class with specified platform settings.

#### Parameters 
* `settings` 

The MCDConnectedDevicesPlatformSettings object which stores the app's settings of the platform.

#### Returns

Returns an MCDConnectedDevicesPlatform object containing the app's platform settings.

### initWithSettings
`- (nullable instancetype)initWithSettings:(MCDConnectedDevicesPlatformSettings* _Nonnull)settings;`

A new instance of this class with the platform settings.

#### Parameters 
* `settings` 

The MCDConnectedDevicesPlatformSettings object which stores the app's settings of the platform.

#### Returns

Returns an MCDConnectedDevicesPlatform object initialized with the app's platform settings.

## Methods

### processNotification
`- (MCDConnectedDevicesProcessNotificationOperation* _Nonnull)processNotification:(NSDictionary* _Nonnull)notification;`

Process incoming APNs notification.

#### Parameters 
* `notification` 

Contains the APNs notification to process.

#### Returns

An instance of the MCDConnectedDevicesProcessNotificationOperation class.

### start
`- (void) start;`

Start the platform.

### shutdownAsync
`- (void)shutdownAsync:(void (^_Nonnull)(NSError* _Nullable))completionBlock;`

Shuts down the Connected Devices Platform.

#### Parameters 
* `completionBlock` 

The block to invoke upon completion.