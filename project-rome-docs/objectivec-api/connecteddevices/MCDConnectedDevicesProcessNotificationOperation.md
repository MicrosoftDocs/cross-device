---
title: MCDConnectedDevicesProcessNotificationOperation
description: The result of giving a notification to the Rome platform for processing.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesProcessNotificationOperation` 

```
@interface MCDConnectedDevicesProcessNotificationOperation : NSObject
```  
The result of giving a notification to the Rome platform for processing.

## Properties

### connectedDevicesNotification
`@property(nonatomic, readonly, getter=isConnectedDevicesNotification) BOOL connectedDevicesNotification;`

The notification that will be handled by the Connected Devices Platform.

## Methods

### waitForCompletionAsync
`- (void)waitForCompletionAsync:(nonnull void (^)(NSError* _Nullable error))callback;`

 Wait for the notification to finish being handled.

#### Parameters 
* `callback` 

The callback result for notification completion.