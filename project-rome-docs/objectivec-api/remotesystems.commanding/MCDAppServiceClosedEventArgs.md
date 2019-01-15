---
title: MCDAppServiceClosedEventArgs
description: Returned by MCDAppServiceConnection.serviceClosed to inform that the MCDAppServiceConnection has been closed and provide a reason behind the close event.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDAppServiceClosedEventArgs` 

```
@interface MCDAppServiceClosedEventArgs : NSObject
```  

Returned by MCDAppServiceConnection.serviceClosed to inform that the MCDAppServiceConnection has been closed and provide a reason behind the close event.

## Properties

### status
`@property(nonatomic, readonly) MCDAppServiceClosedStatus status;`

The status of how the app service closed.