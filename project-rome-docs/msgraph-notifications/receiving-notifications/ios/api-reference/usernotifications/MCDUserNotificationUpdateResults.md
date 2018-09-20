---
title: MCDUserNotificationUpdateResults
description: This class describes the status of an attempt to update a notification.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationUpdateResults`

```
@interface MCDUserNotificationUpdateResults : NSObject
```

This class describes the status of an attempt to update a notification.

## Properties

### notificationId
`@property(nonatomic, readonly, nonnull) NSString* notificationId;`

The ID of the notification.

### succeeded
`@property(nonatomic, readonly) Succeeded succeeded;`

Whether the operation succeeded. 