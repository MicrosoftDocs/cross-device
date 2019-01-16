---
title: MCDRemoteSystemLocalVisibilityKindFilter
description: A class used to set the local (calling) application visibility preference when discovering remote systems.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemLocalVisibilityKindFilter` 

```
@interface MCDRemoteSystemLocalVisibilityKindFilter : NSObject <MCDRemoteSystemFilter>
```  

A class used to set the local (calling) application visibility preference when discovering remote systems.

## Properties

### kind
`@property(nonatomic, readonly) MCDRemoteSystemLocalVisibilityKind kind;`

The visibility setting to filter with.

## Constructors

### filterWithKind
`+ (nullable instancetype)filterWithKind:(MCDRemoteSystemLocalVisibilityKind)localVisibilityKind;`

Creates and initializes an instance of this class.

#### Parameters
* `localVisibilityKind` An MCDRemoteSystemLocalVisibilityKind value indicating the local app visibility setting to filter with.

#### Returns
Returns an MCDRemoteSystemLocalVisibilityKind object filtered by kind.

### initWithKind
`- (nullable instancetype)initWithKind:(MCDRemoteSystemLocalVisibilityKind)localVisibilityKind;`

Creates and initializes an instance of this class.

#### Parameters
* `localVisibilityKind` An MCDRemoteSystemLocalVisibilityKind value indicating the local app visibility setting to filter with.

#### Returns
Returns an MCDRemoteSystemLocalVisibilityKind object initialized with kind.