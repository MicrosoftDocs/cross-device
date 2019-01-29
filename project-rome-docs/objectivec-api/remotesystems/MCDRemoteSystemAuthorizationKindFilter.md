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

A new instance of this class filtered on MCDRemoteSystemAuthorizationKind.

#### Parameters 
* `authorizationKind` 

The authorization type to filter for.

#### Returns
Returns an MCDRemoteSystemAuthorizationKindFilter object with the provided authorization filter.

### initWithKind
`- (nullable instancetype)initWithKind:(MCDRemoteSystemAuthorizationKind)authorizationKind;`

A new instance of this class with MCDRemoteSystemAuthorizationKind.

#### Parameters 
* `authorizationKind` 

The authorization type to filter for.

#### Returns
Returns an MCDRemoteSystemAuthorizationKindFilter object initialized with the authorizationKind.