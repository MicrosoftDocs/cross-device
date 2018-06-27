---
title: MCDRemoteSystemLocalVisibilityKindFilter
description: A class used to set the local (calling) application visibility preference when discovering remote systems.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemLocalVisibilityKindFilter` 

```
@interface MCDRemoteSystemLocalVisibilityKindFilter : NSObject <MCDRemoteSystemFilter>
```  

A class used to set the local (calling) application visibility preference when discovering remote systems.

## Properties

### localVisibilityKind
`@property(nonatomic, readonly) MCDRemoteSystemLocalVisibilityKind localVisibilityKind;`

The visibility setting to filter with.

## Constructors

### filterWithLocalVisibilityKind
`+ (nullable instancetype)filterWithLocalVisibilityKind:(MCDRemoteSystemLocalVisibilityKind)localVisibilityKind;`

Creates and initializes an instance of this class.

#### Parameters
* `localVisibilityKind` An MCDRemoteSystemLocalVisibilityKind value indicating the local app visibility setting to filter with.