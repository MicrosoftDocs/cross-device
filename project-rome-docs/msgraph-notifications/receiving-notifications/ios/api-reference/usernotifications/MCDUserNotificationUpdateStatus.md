---
title: MCDUserNotificationUpdateStatus
description: This class describes the status of an attempt to update a notification.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationUpdateStatus`

```
@interface MCDUserNotificationUpdateStatus : NSObject
```

This class describes the status of an attempt to update a notification.

## Properties

### notificationId
`@property(nonatomic, readonly, nonnull) NSString* notificationId;`

The ID of the notification.

### result
`@property(nonatomic, readonly) MCDUserNotificationResult result;`

The result status of the operation.
