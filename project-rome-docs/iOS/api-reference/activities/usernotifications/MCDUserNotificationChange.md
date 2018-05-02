---
title: MCDUserNotificationChange
description: This class represents the change in state of a notification.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationChange`

```
@interface MCDUserNotificationChange : NSObject
```

This class represents the change in state of a notification.

## Properties

### notification
`@property(nonatomic, readonly, nonnull) MCDUserNotification* notification;`

The underlying notification.

### changeType
`@property(nonatomic, readonly) MCDUserNotificationChangeType changeType;`

The type of notification change.

### changeTime
`@property(nonatomic, readonly, nonnull) NSDate* changeTime;`

The time that the change occurred.
