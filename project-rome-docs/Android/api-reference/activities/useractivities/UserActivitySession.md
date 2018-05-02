---
title: UserActivitySession
description: This class tracks a user activity ([UserActivity](UserActivity.md) instance) while the user is engaged in that activity.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivitySession class

```
public final class UserActivitySession
```

This class tracks a user activity ([UserActivity](UserActivity.md) instance) while the user is engaged in that activity.

A [UserActivity](UserActivity.md) is associated with an UserActivitySession which tracks how long the user is engaged in that activity. For example, an activity such as watching a movie can occur on-and-off over the course of multiple days. When the user first starts the new activity of watching a movie, a UserActivitySession must be created. It should be disposed when the user switches to a different activity. When the user resumes, the app should create another **UserActivitySession** from the original [UserActivity](UserActivity.md) to track the activity as long as the user is watching the movie.

## Methods

### getActivityId
`public String getActivityId()`

Gets a unique ID for this UserActivitySession.

#### Returns
the ID String.

### close
`public void close()`

Closes this activity session. This should be called when the user is no longer engaged in the activity associated with this session.