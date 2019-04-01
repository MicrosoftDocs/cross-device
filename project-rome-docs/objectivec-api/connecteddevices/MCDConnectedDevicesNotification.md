---
title: MCDConnectedDevicesNotification
description: Result of processing a notification. 
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotification` 

```
@interface MCDConnectedDevicesNotification : NSObject
```  
Result of processing a notification.

## Methods

### tryParse

`+ (nullable instancetype)tryParse:(NSDictionary* _Nonnull)dictionary;`

Attempts to parse a MCDConnectedDevicesNotification from an APNS formatted map.

#### Parameters 
* `dictionary` 

The map received from the APNS notification to the Connected Devices platform for processing.
