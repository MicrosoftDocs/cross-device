---
title: MCDRemoteSystemPlatformFilter
description: A class used to filter remote systems based on the OS platform they are running.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemPlatformFilter` 

```
@interface MCDRemoteSystemPlatformFilter : NSObject<MCDRemoteSystemFilter> 
```  

A class used to filter remote systems based on the OS platform they are running.

## Properties

### platform
`@property(nonatomic, readonly) MCDRemoteSystemPlatform platform;`

A MCDRemoteSystemPlatform value indicating the platform to filter for.

## Constructors

### filterWithPlatform
`+ (nullable instancetype)filterWithPlatform:(MCDRemoteSystemPlatform)platform;`

#### Parameters 
* `platform` 

A MCDRemoteSystemPlatform value indicating the platform to filter for.

#### Returns
Returns an MCDRemoteSystemPlatformFilter object filtered by platform.

### initWithPlatform
`- (nullable instancetype)initWithPlatform:(MCDRemoteSystemPlatform)platform;`

#### Parameters 
* `platform` 

A MCDRemoteSystemPlatform value indicating the platform to filter for.

#### Returns
Returns an MCDRemoteSystemPlatformFilter object initialized with a filter by platform.