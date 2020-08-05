---
title: MCDRemoteSystemKindFilter
description: Learn about the MCDRemoteSystemKindFilter class. This class is used to filter remote systems based upon device kind.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemKindFilter` 

```
@interface MCDRemoteSystemKindFilter : NSObject <MCDRemoteSystemFilter>
```  

A class used to filter remote systems based upon device kind.

## Properties

### kinds
`@property(nonatomic, readonly, copy, nonnull) NSArray<NSString*>* kinds;`

An array of strings indicating the kinds of device to filter for.

## Constructors

### filterWithKinds
`+ (nullable instancetype)filterWithKinds:(nonnull NSArray<NSString*>*)kinds;`

A new instance of this class filtered on kinds.

#### Parameters 
* `kinds`

 An array of strings indicating the device kinds to filter for.

#### Returns
Returns an MCDRemoteSystemKindFilter object filtered with kinds.

### initWithKinds
`- (nullable instancetype)initWithKinds:(nonnull NSArray<NSString*>*)kinds;`

A new instance of this class filtered on kinds.

#### Parameters 
* `kinds` 

An array of strings indicating the device kinds to filter for.

#### Returns
Returns an MCDRemoteSystemKindFilter object initialized with kinds.