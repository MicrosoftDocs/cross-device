---
title: MCDConnectedDevicesNotificationRegistrationStatus
description: Learn about the MCDConnectedDevicesNotificationRegistrationStatus class. These values are used to communicate the status of cloud registration.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistrationStatus` 

```
typedef NS_ENUM(NSInteger, MCDConnectedDevicesNotificationRegistrationStatus)
```  
Enumeration indicating the status of the registration operation.
The error statuses indicate transient conditions where the app developer may want to retry registration.

## Fields

| Name                              |   Value     | Description |
|:----------------------------------|:------|:-------------------------------|
| MCDConnectedDevicesNotificationRegistrationStatusSuccess | 0 | Operation completed successfully.
| MCDConnectedDevicesNotificationRegistrationStatusErrorNoNetwork | 1 | Network was unavailable. |
| MCDConnectedDevicesNotificationRegistrationStatusErrorWebFailure | 2 | A web service failed. |
| MCDConnectedDevicesNotificationRegistrationStatusErrorNoTokenRequestSubscriber | 3 | No token request subscribers responded. |
| MCDConnectedDevicesNotificationRegistrationStatusErrorTokenRequestFailed | 4 | The token request failed. |
| MCDConnectedDevicesNotificationRegistrationStatusErrorAccountNotFound | 5 | Account to register information for was not found. |
| MCDConnectedDevicesNotificationRegistrationStatusErrorUnknown | 6 | Operation encountered an unknown error. |