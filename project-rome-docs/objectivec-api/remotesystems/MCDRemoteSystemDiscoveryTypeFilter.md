---
title: MCDRemoteSystemDiscoveryTypeFilter
description: A class used to filter remote systems based upon discovery type.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemDiscoveryTypeFilter` 

```
@interface MCDRemoteSystemDiscoveryTypeFilter : NSObject<MCDRemoteSystemFilter>
```  

A class used to filter remote systems based upon discovery type.

## Properties

### type
`@property(nonatomic, readonly) MCDRemoteSystemDiscoveryType type;`

The discovery type to filter for.

> Note: On Android, the Connected Devices Platform can only use Bluetooth on systems running Android 8.0 (Oreo) or later.

## Constructors

### filterWithType
`+ (nullable instancetype)filterWithType:(MCDRemoteSystemDiscoveryType)discoveryType;`

#### Parameters 
* `discoveryType` The discovery type to filter for.

#### Returns
A new instance of this class with the given type value. Values can be AND'ed together to apply multiple filters at once.

### initWithType
`- (nullable instancetype)initWithType:(MCDRemoteSystemDiscoveryType)discoveryType;`

#### Parameters 
* `discoveryType` The discovery type to filter for.

#### Returns
A new instance of this class with the given type value. Values can be AND'ed together to apply multiple filters at once.

> Note: On Android, the Connected Devices Platform can only use Bluetooth on systems running Android 8.0 (Oreo) or later.