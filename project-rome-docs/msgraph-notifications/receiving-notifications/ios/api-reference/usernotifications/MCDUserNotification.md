---
title: MCDUserNotification
description: This class represents a user notification created by the user's notification channel.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotification`

```
@interface MCDUserNotification : NSObject
```

This class represents a user notification created by the user's notification channel.

## Properties

### notificationId
`@property(nonatomic, readonly, nonnull) NSString* notificationId;`
A unique identifier for the notification.

### groupId
`@property(nonatomic, readonly, nonnull) NSString* groupId;`
The group ID.

### expirationTime
`@property(nonatomic, readonly, nonnull) NSDate* expirationTime;`
The notification's expiration time.

### priority
`@property(nonatomic, readonly) MCDUserNotificationPriority priority;`
The priority attribute of the notification.

### content
`@property(nonatomic, readonly, nonnull) NSString* content;`
The text content of the notification.

###  readState
`@property(nonatomic, readwrite) MCDUserNotificationReadState readState;`
The read state of the notification

### userActionState
`@property(nonatomic, readwrite) MCDUserNotificationUserActionState userActionState;`
The user action state of the notification (what action the user has taken on it).

## Methods

### saveAsync
`- (void)saveAsync:(nonnull void (^)(MCDUserNotificationUpdateStatus* _Nullable, NSError* _Nullable))completion;`

Attempts to save the notification.

#### Parameters
* `completion` The code block to execute upon completion.