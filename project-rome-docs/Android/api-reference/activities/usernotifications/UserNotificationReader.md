---
title: UserNotificationReader
description: This class is used to get the results of a notification query.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationReader class

```
public class UserNotificationReader
```

This class is used to get the results of a notification query (notification data).


## Methods

### readBatchAsyncWithMaxSize
`public AsyncOperation<UserNotification[]> readBatchAsync(@IntRange(from = 0) long maxBatchSize)`

Gets the user notifications, up to the given batch size.

#### Parameters
* `maxBatchSize` The maximum number of notifications to get. A value of 0 gets all available notifications.

#### Returns
An asynchronous operation with an array of [UserNotification](UserNotification.md) instances representing the retrieved notifications.