---
title: MCDRemoteSystemStatusTypeFilter
description: A class used to filter remote systems based on availability status type.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemStatusTypeFilter`

```
@interface MCDRemoteSystemStatusTypeFilter : NSObject <MCDRemoteSystemFilter>
```

A class used to filter remote systems based on availability status type.

## Properties

### type
`@property(nonatomic, readonly) MCDRemoteSystemStatusType type;`
The remote system status type of this filter instance.

## Constructors

### filterWithType
`+ (nullable instancetype)filterWithType:(MCDRemoteSystemStatusType)statusType;`

#### Parameters 
* `statusType` A value indicating the availability status type to filter for.

#### Returns
A new instance of this class with the given type filter.

### initWithType
`- (nullable instancetype)initWithType:(MCDRemoteSystemStatusType)statusType;`

#### Parameters 
* `statusType` A value indicating the availability status type to filter for.

#### Returns
A new instance of this class with the given type filter.