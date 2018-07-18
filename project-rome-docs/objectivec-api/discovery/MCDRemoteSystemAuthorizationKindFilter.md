---
title: MCDRemoteSystemAuthorizationKindFilter
description: A class used to filter remote systems based on authorization type.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemAuthorizationKindFilter` 

```
@interface MCDRemoteSystemAuthorizationKindFilter : NSObject <MCDRemoteSystemFilter>
```  

A class used to filter remote systems based on authorization type.

## Properties

### authorizationKind
`@property(nonatomic, readonly) MCDRemoteSystemAuthorizationKind authorizationKind;`

The authorization type to filter for.

## Constructors

### filterWithAuthorizationKind
`+ (nullable instancetype)filterWithAuthorizationKind:(MCDRemoteSystemAuthorizationKind)authorizationKind;`

#### Parameters 
* `authorizationKind` The authorization type to filter for.

#### Returns
A new instance of this class with the given authorization filter.

### initWithAuthorizationKind
`- (nullable instancetype)initWithAuthorizationKind:(MCDRemoteSystemAuthorizationKind)authorizationKind;`

#### Parameters 
* `authorizationKind` The authorization type to filter for.

#### Returns
A new instance of this class with the given authorization filter.