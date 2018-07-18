---
title: MCDUserNotificationFilter
description: This class is a filter used for querying user notifications.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationFilter`

```
@interface MCDUserNotificationFilter : NSObject
```

This class is a filter used for querying user notifications.

## Properties

### readStateFilter
`@property(nonatomic, readonly) MCDUserNotificationReadStateFilter readStateFilter;`

The filter for read state. 

### userActionStateFilter
`@property(nonatomic, readonly) MCDUserNotificationUserActionStateFilter userActionStateFilter;`

The filter for user action state.

## Constructors

### userNotificationFilterWithReadStateFilter
`+ (nullable instancetype)userNotificationFilterWithReadStateFilter:(MCDUserNotificationReadStateFilter)readStateFilter
                                             userActionStateFilter:(MCDUserNotificationUserActionStateFilter)userActionStateFilter;`

Creates an instance of this class with sub-filter values
#### Parameters
* `readStateFilter` The read state to filter for.
* `userActionStateFilter` The user action state to filter for.

#### Returns
A new instance of this class.
