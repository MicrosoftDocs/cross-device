---
title: MCDRemoteSystem
description:  Contains values that describe the status of a response message from a remote app service.
keywords: microsoft, windows, project rome, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystem` 

```
@interface MCDRemoteSystem : NSObject
```  

A class to represent a remote system.

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
id | The identifier for this remote system.
displayName | The friendly display name of this remote system.
kind | The device type of this remote system.
isAvailableByProximity | Indicates whether the remote system can be reached by proximal connection (UDP or Bluetooth).
status | The availability of the remote system.

## Properties

### id
`@property (nonatomic, readonly, copy, nonnull) NSString* id;`

The identifier for this remote system.

### displayName
`@property (nonatomic, readonly, copy, nonnull) NSString* displayName;`

The friendly display name of this remote system.

### kind
`@property (nonatomic, readonly) MCDRemoteSystemKind kind;`

The device type of this remote system.

### isAvailableByProximity
`@property (nonatomic, readonly) BOOL isAvailableByProximity;`

Indicates whether the remote system can be reached by proximal connection (UDP or Bluetooth).

### status
`@property (nonatomic, readonly) MCDRemoteSystemStatus status;`

The availability of the remote system.