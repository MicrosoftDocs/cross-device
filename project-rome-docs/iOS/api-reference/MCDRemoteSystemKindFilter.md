---
title: MCDRemoteSystemKindFilter
description:  Contains values that describe the status of a response message from a remote app service.
keywords: microsoft, windows, project rome, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemKindFilter` 

```
@interface MCDRemoteSystemKindFilter : NSObject<MCDRemoteSystemFilter>
```  

A class used to filter remote systems based upon device kind.

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
initWithKindsArray | Initializes the filter with an array of kinds to match for.

## Methods

### initWithKindsArray
`-(nullable instancetype)initWithKindsArray:(nonnull NSArray*)kinds;`

Adds a device type to the set of types allowed by this filter.

#### Parameters
* `kinds` An array of device kinds to match with the filter. These should be values provided by the [MCDRemoteSystemKind](MCDRemoteSystemKind.md) enum.
