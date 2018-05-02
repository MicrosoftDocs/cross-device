---
title: UserNotificationChange
description: This class represents the change in the state of a notification.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationChange class

```
public class UserNotificationChange
```

This class represents the change in the state of a notification.

## Methods

### getNotification
`public UserNotification getNotification()`

Gets the underlying notification.

#### Returns
A [UserNotification](UserNotification.md) instance representing the notification.

### getChangeType
`public UserNotificationChangeType getChangeType()`

Gets the type of notification change.

#### Returns
A [UserNotificationChangeType](UserNotificationChangeType.md) value describing the type of change.

### getChangeTime
`public Date getChangeTime()`

Gets the date/time that the change occurred.

#### Returns 
A Date instance representing the time.