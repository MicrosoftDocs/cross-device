---
title: MCDConnectedDevicesProcessNotificationOperation
description: The result of giving a notification to the Rome platform for processing.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesProcessNotificationOperation` 

```
@interface MCDConnectedDevicesProcessNotificationOperation : NSObject
```  
The result of giving an APNS notification to the Connected Devices platform for processing.

> [!NOTE] 
> This class is deprecated, use MCDConnectedDevicesNotification instead. 

## Properties

### connectedDevicesNotification
`@property(nonatomic, readonly, getter=isConnectedDevicesNotification) BOOL connectedDevicesNotification;`

This is a flag indicating whether the notification was intended for the Connected Devices platform.

## Methods

### waitForCompletionAsync
`- (void)waitForCompletionAsync:(nonnull void (^)(NSError* _Nullable error))callback;`

 Wait for the notification to finish being handled.

#### Parameters 
* `callback` 

The callback result for notification completion.
