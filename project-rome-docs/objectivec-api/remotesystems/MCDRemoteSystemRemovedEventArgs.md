---
title: MCDRemoteSystemRemovedEventArgs
description: Event arguments for the RemoteSystemWatcher RemoteSystemRemoved event.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemRemovedEventArgs` 

```
@interface MCDRemoteSystemRemovedEventArgs : NSObject
```  

Event arguments for the MCDRemoteSystemWatcher.remoteSystemRemoved event.

## Properties

### remoteSystem
`@property(nonatomic, readonly, nonnull) MCDRemoteSystem* remoteSystem;`

The MCDRemoteSystem remote system that was removed. This remote system should
not be used after this event.