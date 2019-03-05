---
title: MCDUserActivityChannel
description: This class handles the adding and querying of user activities for the application.
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserActivityChannel`

```
@interface MCDUserActivityChannel : NSObject
```

This class handles the adding and querying of user activities for the application.

## Properties

### syncScope
`@property(class, readonly, nonnull) id<MCDUserDataFeedSyncScope> syncScope;`

Gets the user data sync scope value for User Activities.

### appDisplayName
`@property(nonatomic, copy, nullable) NSString* appDisplayName;`

The display name of the app for all activities.

## Constructors

### channelWithUserDataFeed
`+ (nullable instancetype)channelWithUserDataFeed:(nonnull MCDUserDataFeed*)userDataFeed;`

Creates an instance of this class with the user data feed.

#### Parameters
* `userDataFeed` 
The user data associated with the activities on this channel.

#### Returns
Returns a new instance of this class.

## Methods

### getOrCreateUserActivityAsync
`- (void)getOrCreateUserActivityAsync:(nonnull NSString*)activityId
                          completion:(nonnull void (^)(MCDUserActivity* _Nonnull, NSError* _Nullable))completionBlock;`

Creates the specified user activity, or gets a reference to it if it already exists.

#### Parameters
* `activityId` The ID for this activity.
* `completionBlock` The code block to execute upon completion. This provides access to the retrieved activity.

### deleteActivityAsync
`- (void)deleteActivityAsync:(nonnull NSString*)activityId completion:(nonnull void (^)(NSError* _Nullable))completionBlock;`

Deletes the given user activity.

#### Parameters
* `activityId` The ID of the activity to delete.
* `completionBlock` The code block to execute upon completion.

### deleteAllActivitiesAsync
`- (void)deleteAllActivitiesAsync:(nonnull void (^)(NSError* _Nullable))completionBlock;`

Deletes all user activities.

#### Parameters
* `completionBlock` The code block to execute upon completion.

### getRecentUserActivitiesAsync
`- (void)getRecentUserActivitiesAsync:(NSInteger)maxUniqueActivities
                          completion:(void (^_Nonnull)(NSArray<MCDUserActivitySessionHistoryItem*>* _Nonnull, NSError* _Nullable))completionBlock;`

Gets a history of recent user activities. 

#### Parameters
* `maxUniqueActivities` The maximum number of user activities to retrieve.
* `completionBlock` The code block to execute upon completion. This provides access to the activity history.

### getSessionHistoryItemsForUserActivityAsync
`- (void)getSessionHistoryItemsForUserActivityAsync:(nonnull NSString*)activityId
                                     withStartTime:(nonnull NSDate*)startTime
                                        completion:(void (^_Nonnull)(NSArray<MCDUserActivitySessionHistoryItem*>* _Nonnull, NSError* _Nullable))completionBlock;`

Gets the session history entries for a given activity.

#### Parameters
* `activityId` The ID of the activity to get history for.
* `startTime` The time at which to consider session history.
* `completionBlock` The code block to execute upon completion. This provides access to the activity history.

### getRecentSessionHistoryItemsForTimeRangeAsync
`- (void)getRecentSessionHistoryItemsForTimeRangeAsync:(nonnull NSDate*)startTime
                                 endTime:(nonnull NSDate*)endTime
                                 maxActivities:(NSInteger)maxActivities
                                 completion:(void (^_Nonnull)(NSArray<MCDUserActivitySessionHistoryItem*>* _Nonnull,
                                                       NSError* _Nullable))completionBlock;`

Gets the session history entries for a given activity.

#### Parameters
* `startTime` The time at which to start considering session history.
* `endTime` The time at which to end considering session history.
* `maxActivities` The maximum number of user activities to retrieve.
* `completion` The code block to execute upon completion.
* `completionBlock` The code block to execute upon completion. This provides access to the activity history.