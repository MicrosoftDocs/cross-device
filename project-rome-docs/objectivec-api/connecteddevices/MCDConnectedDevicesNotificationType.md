---
title: MCDConnectedDevicesNotificationType
description:  Contains values that describe the type (service) of a notification.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDConnectedDevicesNotificationType`

```
typedef NS_ENUM(NSInteger, MCDConnectedDevicesNotificationType)
```  
Contains values that describe the type (service) of a notification.

## Fields

| Name                              |   Value     | Description |
|:----------------------------------|:------|:-------------------------------|
| MCDNotificationTypeUnknown | 0 | ConnectedDevicesNotificationType is unknown (consistent with core). |
| MCDNotificationTypeWNS | 1 | Windows Push Notification Services. |
| MCDNotificationTypeGCM | 2 | Google Cloud Messaging. |
| MCDNotificationTypeFCM | 3 | Firebase Cloud Messaging.|
| MCDNotificationTypeAPN | 4 | Apple Push Notification Service. |
| MCDNotificationTypePolling | 5 | No cloud notification service; instead poll for incoming responses. |
