---
title: MCDUserNotificationChannel
description: This class manages the life cycle of user notifications.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationChannel`

```
@interface MCDUserNotificationChannel : NSObject
```

This class manages the life cycle of user notifications.

## Constructors

### userNotificationChannelWithAccount
`+ (nullable instancetype)userNotificationChannelWithAccount:(nonnull MCDUserAccount*)userAccount;`

#### Parameters 
* `userAccount`

#### Returns
A new instance of this class.

## Methods

### addDataChangedListener
`- (NSUInteger)addDataChangedListener:(nonnull void (^)(
                                         MCDUserNotificationChannel* _Nonnull, MCDUserNotificationChangeReader* _Nonnull))listener;`

Adds a listener to the data changed event, which is raised whenever the user notification data changes.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
A unique identifier for this event registration.

### removeDataChangedListener
`- (void)removeDataChangedListener:(NSUInteger)eventRegistrationToken;`

Removes a listener to the data changed event, which is raised whenever the user notification data changes.

#### Parameters 
* `eventRegistrationToken` The event registration ID of the listener to remove.

### createReaderWithFilter
`- (MCDUserNotificationReader* _Nullable)createReaderWithFilter:(nonnull MCDUserNotificationFilter*)filter;`

#### Parameters
* `filter` A filter to limit the set of notifications received by this reader.

#### Returns
The notification reader.


### createChangeReaderAsyncForState
`- (void)createChangeReaderAsyncForState:(NSString* _Nullable)state
                             completion:(nonnull void (^)(MCDUserNotificationChangeReader* _Nullable, NSError* _Nullable))completion;`

Gets a new MCDUserNotificationChangeReader to monitor notification changes.

#### Parameters
* `state` [optional] The state of the reader, to allow the reader to start from an advanced position and receive only the changes to notifications that have not already been accepted.
* `completion` The code block to execute upon completion. This provides access to the new MCDUserNotificationChangeReader object.


### getUserNotificationAsync
`- (void)getUserNotificationAsync:(nonnull NSString*)notificationId
                      completion:(nonnull void (^)(MCDUserNotification* _Nullable, NSError* _Nullable))completion;`

Obtains the UserNotification object associated with the given notification ID.

#### Parameters
* `notificationId` The ID of the notification.
* `completion` The code block to execute upon completion. This provides access to the new MCDUserNotification object.


### deleteUserNotificationAsync
`- (void)deleteUserNotificationAsync:(NSString* _Nonnull)notificationId
                         completion:(nonnull void (^)(MCDUserNotificationUpdateStatus* _Nullable, NSError* _Nullable))completion;`

Deletes the UserNotification object associated with the given notification ID.

#### Parameters
* `notificationId` The ID of the notification.
* `completion` The code block to execute upon completion.