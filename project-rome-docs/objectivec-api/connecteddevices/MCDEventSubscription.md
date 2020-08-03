---
title: MCDEventSubscription
description: Learn about the 'MCDEventSubscription' class. This interface provides a simple way to manage an event subscription.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDEventSubscription` 

```
@interface MCDEventSubscription : NSObject
```  
This interface provides a simple event subscription.

## Methods

### cancel
`- (void)cancel;`

Cancels an event subscription. After making this call, the attached EventListener will
not receive any more events (Already in flight events may still be delivered).
Because much of the ConnectedDevices functionality is done in native code, it is important
to either always ensure cancel is called or WeakReferences are used to ensure proper clean up
of resources held by the EventListener.
