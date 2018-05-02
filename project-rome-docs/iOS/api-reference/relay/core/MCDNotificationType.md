---
title: MCDNotificationType
description: Contains values that describe the type (platform) of a notification.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# enum `MCDNotificationType`

```
typedef NS_ENUM(NSInteger, MCDNotificationType)
```

Contains values that describe the type (platform) of a notification.

|Name | Value | Description |
|:-- |:-- |:-- |
|MCDNotificationTypeNone |0 | No known notification service.
|MCDNotificationTypeWNS |1| Windows Push Notification Services.
|MCDNotificationTypeGCM |2| Google Cloud Messaging.
|MCDNotificationTypeFCM |3| Firebase Cloud Messaging.
|MCDNotificationTypeAPN |4| Apple Push Notification Service.