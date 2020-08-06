---
title: MCDRemoteSystem
description: Learn about the MCDRemoteSystem class and its properties. This class is used to represent a remote system.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystem` 

```
@interface MCDRemoteSystem : NSObject
```  

A class to represent a remote system.

## Properties

### kind
`@property(nonatomic, readonly, nonnull) NSString* kind;`

The device type of this remote system.

### systemId
`@property(nonatomic, readonly, nonnull) NSString* systemId;`

The identifier for this remote system.

### displayName
`@property(nonatomic, readonly, nonnull) NSString* displayName;`

The name of the given remote system.

### status
`@property(nonatomic, readonly) MCDRemoteSystemStatus status;`

The status of this remote system's availability.

> [!NOTE]
WNS presence is used for reporting availability for Windows devices and apps which use WNS as notification type.  RemoteSystem will be marked as "available" when the device is considered available (Windows) or when one of the underlying apps reports their presence as available (iOS and Android). 

### manufacturerDisplayName
`@property(nonatomic, readonly, nonnull) NSString* manufacturerDisplayName;`

The manufacturer name of the given remote system.

### modelDisplayName
`@property(nonatomic, readonly, nonnull) NSString* modelDisplayName;`

The model name of the given remote system.

### apps
`@property(nonatomic, readonly, nonnull) NSArray<MCDRemoteSystemApp*>* apps;`

An array of the applications on this remote system that are available for connectivity.

### platform
`@property(nonatomic, readonly) MCDRemoteSystemPlatform platform;`

The MCDRemoteSystemPlatform managing remote system activity.