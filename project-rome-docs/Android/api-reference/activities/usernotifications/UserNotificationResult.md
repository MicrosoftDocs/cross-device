---
title: UserNotificationResult
description: Contains values that describe the status of an attempt to update the state of a notification (activate or delete).
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationResult enum

```
public enum UserNotificationResult
```

Contains values that describe the status of an attempt to update the state of a notification (activate or delete).

|Name | Value | Description |
|:-- |:-- |:-- |
|    UNKNOWN |0| The result is unknown.|
|    SUCCESS|1| The notification update was successful.|
|    AUTH_FAILURE|2| The notification update failed due to an authorization issue.|
|    CONFLICT|3| The notification update failed due to conflicting updates.|
