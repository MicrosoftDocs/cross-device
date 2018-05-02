---
title: UserNotificationChannel
description: This class manages the life cycle of user notifications.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationChannel class

```
public class UserNotificationChannel
```

This class manages the life cycle of user notifications.

## Constructors


### UserNotificationChannel
`public UserNotificationChannel(UserAccount account)`

#### Parameters 
* `account` tbd

#### Returns
A new instance of this class.

## Methods

### addDataChangedListener
`public long addDataChangedListener(@NonNull EventListener<UserNotificationChannel, UserNotificationChangeReader> listener)`

Adds a listener to the data changed event, which is raised whenever the user notification data changes.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
A unique identifier for this event registration.

### removeDataChangedListener
`public void removeDataChangedListener(long eventRegistrationToken)`

Removes a listener to the data changed event, which is raised whenever the user notification data changes.

#### Parameters 
* `eventRegistrationToken` The event registration ID of the listener to remove.

### createReader
`public UserNotificationReader createReader(@NonNull UserNotificationFilter filter)`

#### Parameters
* `filter` A filter to limit the set of notifications received by this reader.

#### Returns
The notification reader.


### createChangeReaderAsync
`public AsyncOperation<UserNotificationChangeReader> createChangeReaderAsync(@Nullable String serializedState)`

Gets a new [UserNotificationChangeReader](UserNotificationChangeReader.md) to monitor notification changes.

#### Parameters
* `serializedState` [optional] The state of the reader, to allow the reader to start from an advanced position and receive only the changes to notifications that have not already been accepted.

#### Returns
An asynchronous operation with a [UserNotificationChangeReader](UserNotificationChangeReader.md) instance.

### getUserNotificationAsync
`public AsyncOperation<UserNotification> getUserNotificationAsync(@NonNull String notificationId)`

Obtains the [UserNotification](UserNotification.md) object associated with the given notification ID.

#### Parameters
* `notificationId` The ID of the notification.

#### Returns
An asynchronous operation with a [UserNotification](UserNotification.md) instance.

### deleteUserNotificationAsync
`public AsyncOperation<UserNotificationUpdateStatus> deleteUserNotificationAsync(@NonNull String notificationId)`

Deletes the [UserNotification](UserNotification.md) object associated with the given notification ID.

#### Parameters
* `notificationId` The ID of the notification.

#### Returns
An asynchronous operation with a [UserNotificationUpdateStatus](UserNotificationUpdateStatus.md) value indicating the status of the attempt to delete the notification.