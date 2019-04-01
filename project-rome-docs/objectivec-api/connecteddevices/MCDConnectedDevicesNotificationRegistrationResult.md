---
title: MCDConnectedDevicesNotificationRegistrationResult
description: Communicates the async result of registering notification information for an account. 
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistrationResult` 

```
@interface MCDConnectedDevicesNotificationRegistrationResult : NSObject
```  
MCDConnectedDevicesNotificationRegistrationResult communicates the async result of registering notification information for an account. The error statuses communicated through this result should be used by the app to retry registration in the event of certain transient conditions like the network being unavailable.

## Properties

### status

`@property(nonatomic, readonly) MCDConnectedDevicesNotificationRegistrationStatus status;`

Status enum of the registration operation.