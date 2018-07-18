---
title: MCDRemoteSystemConnectionInfo
description: A class that provides further information about a given MCDAppServiceConnection instance.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemConnectionInfo` 

```
@interface MCDRemoteSystemConnectionInfo : NSObject
```  

A class that provides further information about a given **[MCDAppServiceConnection](MCDAppServiceConnection.md)** instance.

## Properties

### isProximal
`@property(nonatomic, readonly) BOOL isProximal;`

Displays whether the associated connection is a proximal connection (**YES**) or not (**NO**).

## Methods

### tryCreateFromAppServiceConnection
`+ (nullable instancetype)tryCreateFromAppServiceConnection:(nonnull MCDAppServiceConnection*)appServiceConnection;`

Creates an instance of this class from the given app service connection.

#### Parameters
* `appServiceConnection` An **MCDAppServiceConnection** instance.

#### Returns
An instance of this class corresponding to the app service connection.