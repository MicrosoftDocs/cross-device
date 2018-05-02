---
title: UserActivityChannel
description: This class handles the adding and querying of user activities for the application.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivityChannel class

```
public final class UserActivityChannel
```

This class handles the adding and querying of user activities for the application.

## Constructors

### UserActivityChannel
`public UserActivityChannel(@NonNull UserAccount account, @Nullable String activitySourceHost)`

Creates and initializes a new instance of this class.

#### Parameters
* `account` The account of the user whose activities will be accessed by this channel.
* `activitySourceHost` [optional] A String indicating the source of the activities on this channel.

## Methods

### getOrCreateUserActivityAsync
`public AsyncOperation<UserActivity> getOrCreateUserActivityAsync(@NonNull String activityId)`

Creates the specified user activity, or gets a reference to it if it already exists.

#### Parameters
* `activityId` The ID for this activity.

#### Returns
An asynchronous operation with the retrieved activity.

### deleteActivityAsync
` public AsyncOperation<Void> deleteActivityAsync(@NonNull String activityId)`

Deletes the given user activity.

#### Parameters
* `activityId` The ID of the activity to delete.

### deleteAllActivitiesAsync
`public AsyncOperation<Void> deleteAllActivitiesAsync()`

Deletes all user activities.


### getRecentUserActivitiesAsync
`public AsyncOperation<UserActivitySessionHistoryItem[]> getRecentUserActivitiesAsync(int maxUniqueActivities)`

Gets a history of recent user activities. 

#### Parameters
* `maxUniqueActivities` The maximum number of user activities to retrieve.

#### Returns
An asynchronous operation with an array of [UserActivitySessionHistoryItem](UserActivitySessionHistoryItem.md) instances.

### getSessionHistoryItemsForUserActivityAsync
`public AsyncOperation<UserActivitySessionHistoryItem[]> getSessionHistoryItemsForUserActivityAsync(@NonNull String activityId, @NonNull Date startTime)`

Gets the session history entries for a given activity.

#### Parameters
* `activityId` The ID of the activity to get history for.
* `startTime` The time from which to consider session history.

#### Returns
An asynchronous operation with an array of [UserActivitySessionHistoryItem](UserActivitySessionHistoryItem.md) instances.