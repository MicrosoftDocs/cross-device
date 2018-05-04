---
title: UserNotification
description: This class represents a user notification created by the user's notification channel.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotification class

```
public class UserNotification
```

This class represents a user notification created by the user's notification channel.

## Methods

### getId
`public String getId()`

Gets a unique identifier for the notification.

#### Returns
An ID String.

### getGroupId
`public String getGroupId()`
Gets the group ID

#### Returns
The group ID.

### getExpirationTime
`public Date getExpirationTime()`
Gets the notification's expiration time.

#### Returns
The expiration time.

### getContent
`public String getContent()`

Gets the text content of the notification.

#### Returns
The content String.

### getPriority
`public UserNotificationPriority getPriority()`

Gets the priority attribute of the notification.

#### Returns
A [UserNotificationPriority](UserNotificationPriority.md) value describing the priority.

###  getReadState
`public UserNotificationReadState getReadState()`

Gets the read state of the notification

#### Returns
A [UserNotificationReadState](UserNotificationReadState.md) value describing the read state.

### setReadState
`public void setReadState(@NonNull UserNotificationReadState readState)`

Sets the read state of the notification.

#### Parameters
* `readState` The read state to set.

### getUserActionState
`public UserNotificationUserActionState getUserActionState()`

Gets the user action state of the notification (what action the user has taken on it).

#### Returns
A [UserNotificationUserActionState](UserNotificationUserActionState.md) value describing the user action.

### setUserActionState
`public void setUserActionState(@NonNull UserNotificationUserActionState userActionState)`

Sets the recorded user action state of the notification.

#### Parameters
* `userActionState` The [UserNotificationUserActionState](UserNotificationUserActionState.md) value indicating the action state to set.

### saveAsync
`public AsyncOperation<UserNotificationUpdateStatus> saveAsync()`

Attempts to save the notification.

#### Returns
An asynchronous operation with the notification update status.