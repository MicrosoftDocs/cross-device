---
title: UserNotificationFilter
description: This class contains filters used for querying user notifications.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationFilter class

```
public class UserNotificationFilter
```

This class contains filters used for querying user notifications.

## Constructors

### UserNotificationFilter
`public UserNotificationFilter(UserNotificationReadStateFilter readStateFilter, UserNotificationUserActionStateFilter stateFilter)`

Creates an instance of this class with sub-filter values

#### Parameters
* `readStateFilter` The read state to filter for.
* `stateFilter` The user action state to filter for.


## Methods

### getReadStateFilter
`public UserNotificationReadStateFilter getReadStateFilter()`

Gets the notification filter for read state. 

#### Returns
A [UserNotificationReadStateFilter](UserNotificationReadStateFilter.md) value describing how to filter based on read state.

### getUserActionStateFilter
`public UserNotificationUserActionStateFilter getUserActionStateFilter()`

Gets the notification filter for user action state.

#### Returns
A [UserNotificationUserActionStateFilter](UserNotificationUserActionStateFilter.md) value describing how to filter based on user action state.
