---
title: UserActivitySessionHistoryItem
description: This class provides the start and end time that a user was engaged in a particular activity.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivitySessionHistoryItem

```
public final class UserActivitySessionHistoryItem
```

This class provides the start and end time that a user was engaged in a particular activity.

## Methods

### getUserActivity
`public UserActivity getUserActivity()`

Gets the user activity whose history this class instance represents.

#### Returns
A [UserActivity](UserActivity.md) instance representing the activity.

### getStartTime
`public Date getStartTime()`

Gets the time when the user started engaging in the associated activity.

#### Returns
A Date instance indicating the start time.

### getEndTime
`public Date getEndTime()`

Gets the time when the user stopped engaging in the associated activity.

#### Returns
A Date instance indicating the stop time.