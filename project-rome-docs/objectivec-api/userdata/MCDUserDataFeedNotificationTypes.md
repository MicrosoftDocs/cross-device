---
title: MCDUserDataFeedNotificationTypes
description: This class is responsible for providing the notification types
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserDataFeedNotificationTypes`

```
@interface MCDUserDataFeedNotificationTypes : NSObject
```

This class provides the MCDUserDataFeedNotficationTypes.


## Properties

### notificationWithPayload
`@property(class, nonatomic, readonly, nonnull) NSString* notificationWithPayload;`

Represents the incoming push notifications.  There are no rescrictions to push notifications other than domain/server restrictions.

### notificationOnly
`@property(class, nonatomic, readonly, nonnull) NSString* notificationOnly;`

Demote all push notifications to a notification only telling the system to sync to receive the data, even if the data could be contained in the push notification.


### noNotification
`@property(class, nonatomic, readonly, nonnull) NSString* noNotification;`

Prevent any notifications for new user data, only receive new data when UserDataFeed.startSync is called, or when interacting with the server in other ways
