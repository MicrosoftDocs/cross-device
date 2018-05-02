---
title: UserNotificationUserActionStateFilter
description: Contains values that categorize notifications by user action state (for filtered notification retrieval).
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserNotificationUserActionStateFilter enum

```
public enum UserNotificationUserActionStateFilter
```

Contains values that categorize notifications by user action state (for filtered notification retrieval).

|Name | Value | Description |
|:-- |:-- |:-- |
|NONE           |0| Include notifications that have not been acted on by the user.|
|    ACTIVATED  |1| Include notifications that have been activated by the user.|
|    SNOOZED    |2| Include notifications that have been snoozed by the user.|
|   DISMISSED   |3| Include notifications that have been dismissed by the user.|
|   ANY         |4| Include notifications regardless of user action state.|

