---
title: MCDConnectedDevicesNotificationRegistrationState
description: Values used to communicate the status of cloud registration.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistrationState` 

```
typedef NS_ENUM(NSUInteger, MCDConnectedDevicesNotificationRegistrationState)
```  
Values used to communicate the status of cloud registration.

## Fields

| Name                              |   Value     | Description |
|:----------------------------------|:------|:-------------------------------|
| MCDConnectedDevicesNotificationRegistrationStateUnregistered | 0 | Registration has never been started.
| MCDConnectedDevicesNotificationRegistrationStateRegistered | 1 | Registration has finished. |
| MCDConnectedDevicesNotificationRegistrationStateExpiring | 2 | Registration is about to expire and so the app should perform registration again. |
| MCDConnectedDevicesNotificationRegistrationStateExpired | 3 | Registration has expired and so the app must perform registration again. |