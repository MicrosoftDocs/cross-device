---
title: MCDRemoteSystemConnectionRequest
description:  Contains values that describe the status of a response message from a remote app service.
keywords: microsoft, windows, project rome, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemConnectionRequest` 

```
@interface MCDRemoteSystemConnectionRequest : NSObject
```  

A class used to express a connection request intent against a remote system.

## Summary

 Members                        | Descriptions                                
--------------------------------|---------------------------------------------
remoteSystem | The remote system to connect to.
initWithRemoteSystem | Initializes the [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) with a [MCDRemoteSystem](MCDRemoteSystem.md) instance.

## Properties

### remoteSystem
`@property (nonatomic, readonly, strong, nonnull) MCDRemoteSystem* remoteSystem;`

The remote system to connect to.

## Methods

### initWithRemoteSystem
`-(nullable instancetype)initWithRemoteSystem:(nonnull MCDRemoteSystem*)remoteSystem;`

Initializes the [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) with a [MCDRemoteSystem](MCDRemoteSystem.md) instance.