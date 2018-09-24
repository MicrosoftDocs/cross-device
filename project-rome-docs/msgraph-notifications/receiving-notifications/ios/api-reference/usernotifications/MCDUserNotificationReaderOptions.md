---
title: MCDUserNotificationReaderOptions
description: This class allows the app to provide options on the notification reader, such as only receiving new user notifications and not existing notification updates. 
keywords: microsoft, windows, Graph Notifications, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationReaderOptions`

```
@interface MCDUserNotificationReaderOptions : NSObject
```

This class allows the app to provide options on the notification reader, such as only receiving new user notifications and not existing notification updates. 

## Constructors

### userNotificationReaderOptions
`+ (nullable instancetype)userNotificationReaderOptions`
Creates and initializes a new instance of UserNotificationReaderOptions.

### userNotificationReaderOptionsWithStartPosition
`+(nullable instancetype)userNotificationReaderOptionsWithStartPosition`
Creates and initializes a new instance of UserNotificationReaderOptions with filters specified. 

## Properties

### StartPosition
`@property(nonatomic, readwrite) MCDUserNotificationReaderStartPosition startPosition;`
Get or set the start position for this instance of UserNotificationReaderOptions.

### StatusFilter
`@property(nonatomic, readwrite) MCDUserNotificationStatusFilter statusFilter;`
Get or set the status filter for this user notification reader you desire to create.

### ReadStateFilter
`@property(nonatomic, readwrite) MCDUserNotificationReadStateFilter readStateFilter;`
Get or set the read state filter that’s set for this instance of UserNotificationReaderOptions

### UserActionStateFilter
`@property(nonatomic, readwrite) MCDUserNotificationUserActionStateFilter userActionStateFilter;`
Getor set  the user action state filter that’s set for this instance of UserNotificationReaderOptions.

