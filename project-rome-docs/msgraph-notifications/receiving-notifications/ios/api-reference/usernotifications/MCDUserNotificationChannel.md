---
title: MCDUserNotificationChannel
description: This class manages the life cycle of user notifications.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationChannel`

```
@interface MCDUserNotificationChannel : NSObject
```

This class provides the notification change reader which handles the receiving and management of user notifications for the application. 

## Constructors

### userNotificationChannelWithUserDataFeed
`+ (nullable instancetype)userNotificationChannelWithUserDataFeed:(MCDUserDataFeed* _Nonnull)userDataFeed`

### userNotificationChannelWithAccount
`+ (nullable instancetype)userNotificationChannelWithAccount:(nonnull MCDUserAccount*)userAccount;


## Methods

### addDataChangedListener
`- (NSUInteger)addDataChangedListener:(nonnull void (^)(
                                         MCDUserNotificationChannel* _Nonnull, MCDUserNotificationChangeReader* _Nonnull))listener;`

Adds a listener to the data changed event, which is raised whenever the user notification data changes.



### syncScope
`+ (nonnull MCDUserDataFeedSyncScope*)`

Get the sync scope of this user notification channel'

### getUserNotificationAsync
`- (void)getUserNotificationAsync:(NSString* _Nonnull)notificationId
                      completion:(nonnull void (^)(MCDUserNotification* _Nullable, NSError* _Nullable))completion`

Get a user notification based on its id.

### createReader
`- (MCDUserNotificationReader* _Nullable)createReader`

Create a user notification reader to receive and manage user notifications published by app server.

### createReaderWithOptions
`- (MCDUserNotificationReader* _Nullable)createReaderWithOptions:(MCDUserNotificationReaderOptions* _Nonnull)options`

Create a user notification reader with options 

### createReaderWithState
`- (MCDUserNotificationReader* _Nullable)createReaderWithState:(NSString* _Nonnull)readerState`

Create a user notification reader to receive and manage user notifications published by app server. 
The reader will start at the provided tracking state.  

### deleteUserNotificationAsync
`- (void)deleteUserNotificationAsync:(NSString* _Nonnull)notificationId
                         completion:(nonnull void (^)(MCDUserNotificationUpdateResult* _Nullable, NSError* _Nullable))completion`

Delete a user notification based on its id. 

