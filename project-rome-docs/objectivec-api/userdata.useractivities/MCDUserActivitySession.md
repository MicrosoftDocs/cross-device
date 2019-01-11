---
title: MCDUserActivitySession
description: This class tracks a user activity ([MCDUserActivity](MCDUserActivity.md) instance) while the user is engaged in that activity.

keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserActivitySession`

```
@interface MCDUserActivitySession : NSObject
```

This class tracks engagement for a specified user activity ([MCDUserActivity](MCDUserActivity.md) instance).

A [MCDUserActivity](MCDUserActivity.md) is associated with an MCDUserActivitySession which tracks how long the user is engaged in that activity. For example, an activity such as watching a movie can occur on-and-off over the course of multiple days. When the user first starts the new activity of watching a movie, a MCDUserActivitySession must be created. It should be disposed when the user switches to a different activity. When the user resumes, the app should create another **MCDUserActivitySession** from the original [MCDUserActivity](MCDUserActivity.md) to track the activity as long as the user is watching the movie.


## Properties

### activityId
`@property(nonatomic, readonly, nonnull) NSString* activityId;`

A unique ID for the MCDUserActivity associated with this MCDUserActivitySession.

## Methods

### stop
`- (void)stop;`

TODO - Closes this activity session. This should be called when the user is no longer engaged in the activity associated with this session.