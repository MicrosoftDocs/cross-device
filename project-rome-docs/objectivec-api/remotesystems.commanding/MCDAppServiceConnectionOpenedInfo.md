---
title: MCDAppServiceConnectionOpenedInfo
description: This class provides data for the MCDAppServiceProvider.connectionDidOpen event, which is raised when a remote device opens a connection to a local app service.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDAppServiceConnectionOpenedInfo` 

```
@interface MCDAppServiceConnectionOpenedInfo : NSObject
```  

This class provides data for the MCDAppServiceProvider.connectionDidOpen event,
which is raised when a remote device opens a connection to a local app service.

## Properties

### appServiceConnection
`@property(nonatomic, readonly, nonnull) MCDAppServiceConnection* appServiceConnection;`

An MCDAppServiceConnection instance representing the connection between the local app service and the remote device.

### remoteSystemApp
`@property(nonatomic, readonly, nullable) MCDRemoteSystemApp* remoteSystemApp;`

The MCDRemoteSystemApp remote application that initiated a connection to the local app service.