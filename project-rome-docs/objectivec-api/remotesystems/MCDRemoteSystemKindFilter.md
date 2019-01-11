---
title: MCDRemoteSystemKindFilter
description: A class used to filter remote systems based upon device kind.
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

#### Parameters 
* `kinds` An array of strings indicating the device kinds to filter for.

#### Returns
A new instance of this class with the given type filter.

### initWithKinds
`- (nullable instancetype)initWithKinds:(nonnull NSArray<NSString*>*)kinds;`

#### Parameters 
* `kinds` An array of strings indicating the device kinds to filter for.

#### Returns
A new instance of this class with the given type filter.