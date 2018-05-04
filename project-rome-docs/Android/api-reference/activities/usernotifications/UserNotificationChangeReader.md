---
title: UserNotificationChangeReader
description: This class is responsible for retrieving a user's notifications.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationChangeReader class

```
public class UserNotificationChangeReader
```

This class is responsible for retrieving the state changes of a user's notifications.

## Methods

### readBatchAsync
`public AsyncOperation<UserNotificationChange[]> readBatchAsync(@IntRange(from = 0) long maxBatchSize)`

Gets the next batch of notifications from the current query, up to the limit set by the caller.

#### Parameters
* `maxBatchSize` The maximum number of notifications to get. A value of 0 gets all available notifications.

#### Returns
An asynchronous operation with an array of [UserNotificationChange](UserNotificationChange.md) instances, which contain notification data.


### getSerializedState
`public String getSerializedState()`

Gets the current state of the change reader. This can be used to construct a new reader starting from the same state (based upon the last completed batch of notification changes, or the initial state if none have completed successfully).

#### Returns
A serialized String indicating the state.