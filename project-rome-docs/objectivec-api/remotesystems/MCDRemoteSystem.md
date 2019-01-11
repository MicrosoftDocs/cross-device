---
title: MCDRemoteSystem
description: A class to represent a remote system.
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

The friendly display name of this remote system.

### status
`@property(nonatomic, readonly) MCDRemoteSystemStatus status;`

The availability status of the remote system.

### manufacturerDisplayName
`@property(nonatomic, readonly, nonnull) NSString* manufacturerDisplayName;`

The display name of the remote system manufacturer.

### modelDisplayName
`@property(nonatomic, readonly, nonnull) NSString* modelDisplayName;`

The display name of the remote system model.

### apps
`@property(nonatomic, readonly, nonnull) NSArray<MCDRemoteSystemApp*>* apps;`

An array of the applications on this remote system that are available for connectivity.

### platform
`@property(nonatomic, readonly) MCDRemoteSystemPlatform platform;`

The MCDRemoteSystemPlatform managing remote system activity.