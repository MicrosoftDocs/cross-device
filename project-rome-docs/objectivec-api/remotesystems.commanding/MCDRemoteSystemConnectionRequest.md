---
title: MCDRemoteSystemConnectionRequest
description:  A class that represents an attempt to communicate with a specific remote device or application.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemConnectionRequest` 

```
@interface MCDRemoteSystemConnectionRequest : NSObject
```  

A class that represents an attempt to communicate with a specific remote device or application.

## Constructors

### requestWithRemoteSystem
`+ (instancetype)requestWithRemoteSystem:(nonnull MCDRemoteSystem*)remoteSystem;`

Initializes the [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) with a [MCDRemoteSystem](../remotesystems/MCDRemoteSystem.md) instance. This constructor is not recommended, as it does not specify an app to target and therefore may result in an unexpected app being selected to service requests sent to the system.

#### Parameters
* `remoteSystem` 

The remote system to be targeted in this connection request.

#### Returns
Returns the initialized [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) if successful, otherwise nil.

### requestWithRemoteSystemApp
`+ (instancetype)requestWithRemoteSystemApp:(nonnull MCDRemoteSystemApp*)remoteSystemApp;`

Creates and initializes a new instance of this class.

#### Parameters
* `remoteSystemApp` 

The remote app to be targeted in this connection request.

#### Returns
Returns the initialized [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) if successful, otherwise nil.

### initWithRemoteSystem
`- (nullable instancetype)initWithRemoteSystem:(nonnull MCDRemoteSystem*)remoteSystem;`

Initializes the [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) with a [MCDRemoteSystem](../remotesystems/MCDRemoteSystem.md) instance. This constructor is not recommended, as it does not specify an app to target and therefore may result in an unexpected app being selected to service requests sent to the system.

#### Parameters
* `remoteSystem` The remote system to be targeted in this connection request.

#### Returns
Returns the initialized [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) if successful, otherwise nil.

### initWithRemoteSystemApp
`- (nullable instancetype)initWithRemoteSystemApp:(nonnull MCDRemoteSystemApp*)remoteSystemApp;`

Creates and initializes a new instance of this class.

#### Parameters
* `remoteSystemApp` 

The remote app to be targeted in this connection request.

#### Returns
Returns the initialized [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md) if successful, otherwise nil.