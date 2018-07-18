---
title: MCDUserNotificationResult
description: Contains values that describe the status of an attempt to update the state of a notification (activate or delete).

keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# enum `MCDUserNotificationResult`

```
typedef NS_ENUM(NSInteger, MCDUserNotificationResult)
```

Contains values that describe the status of an attempt to update the state of a notification (activate or delete).

|Name | Value | Description |
|:-- |:-- |:-- |
|    MCDUserNotificationResultUnknown |0| The result is unknown.|
|    MCDUserNotificationResultSuccess|1| The notification update was successful.|
|    MCDUserNotificationResultAuthFailure|2| The notification update failed due to an authorization issue.|
|    MCDUserNotificationResultConflict|3| The notification update failed due to conflicting updates.|