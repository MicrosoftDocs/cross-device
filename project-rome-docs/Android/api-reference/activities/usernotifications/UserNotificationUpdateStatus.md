---
title: UserNotificationUpdateStatus
description: This class describes the status of an attempt to update a notification.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationUpdateStatus class

```
public class UserNotificationUpdateStatus
```

This class describes the status of an attempt to update a notification.

## Methods

### getNotificationId
`public String getNotificationId()`

Gets the ID of the notification in question.

#### Returns
The ID String.

### getResult
`public UserNotificationResult getResult()`

Gets the result status of the operation.

#### Returns
A [UserNotificationResult](UserNotificationResult.md) value describing the result status.