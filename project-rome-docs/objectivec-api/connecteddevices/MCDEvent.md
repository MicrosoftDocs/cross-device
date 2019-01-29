---
title: MCDEvent
description:  This interface provides a simple event model. Events produce items consumed by EventListeners.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDEvent` 

```
@interface MCDEvent<__covariant SourceType, __covariant ArgsType> : NSObject
```  
 
 This interface provides a simple event model. Events produce items consumed by EventListeners.
 The flow of event items is controlled by the MCDEventSubscription.

## Methods

### subscribe
`- (nonnull MCDEventSubscription*)subscribe:(nonnull void (^)(SourceType _Nonnull, ArgsType _Nonnull))listener;`

Subscribe to given events in the Connected Devices Platform.

#### Parameters 
* `listener` 

Listen to MCDEventSubscriptions.

#### Returns
An instance of the MCDEventSubscription.