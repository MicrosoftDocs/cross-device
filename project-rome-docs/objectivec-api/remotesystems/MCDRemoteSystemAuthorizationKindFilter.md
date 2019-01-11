---
title: MCDRemoteSystemAuthorizationKindFilter
description: A class used to filter remote systems based on authorization type.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemAuthorizationKindFilter` 

```
@interface MCDRemoteSystemAuthorizationKindFilter : NSObject<MCDRemoteSystemFilter>
```  

A class used to filter remote systems based on authorization type.

## Properties

### kind
`@property(nonatomic, readonly) MCDRemoteSystemAuthorizationKind kind;`

The authorization type to filter for.

## Constructors

### filterWithKind
`+ (nullable instancetype)filterWithKind:(MCDRemoteSystemAuthorizationKind)authorizationKind;`

#### Parameters 
* `authorizationKind` The authorization type to filter for.

#### Returns
A new instance of this class with the given authorization filter.

### initWithKind
`- (nullable instancetype)initWithKind:(MCDRemoteSystemAuthorizationKind)authorizationKind;`

#### Parameters 
* `authorizationKind` The authorization type to filter for.

#### Returns
A new instance of this class with the given authorization filter.