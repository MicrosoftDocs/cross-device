---
title: MCDUserActivitySessionHistoryItem
description: This class provides the start and end time that a user was engaged in a particular activity.
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserActivitySessionHistoryItem`

```
@interface MCDUserActivitySessionHistoryItem : NSObject
```

This class provides the start and end time that a user was engaged in a particular activity.


## Properties

### userActivity
`@property(nonatomic, readonly, nonnull) MCDUserActivity* userActivity;`

The user activity whose history this class instance represents.

### startTime
`@property(nonatomic, readonly, nonnull) NSDate* startTime;`

The time when the user started engaging in the associated activity.

### endTime
`@property(nonatomic, readonly, nullable) NSDate* endTime;`

The time when the user stopped engaging in the associated activity.

### remoteSystemId
`@property(nonatomic, readonly, nullable) NSString* remoteSystemId;`

TODO