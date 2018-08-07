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
`@property(class, readonly, nonnull) MCDUserDataFeedSyncScope* syncScope;`

Gets the user data sync scope value for User Activities.

## Constructors

### userActivityChannelWithUserDataFeed
`+ (nullable instancetype)userActivityChannelWithUserDataFeed:(nonnull MCDUserDataFeed*)userDataFeed;
`

#### Parameters
* `userDataFeed` The user data associated with the activities on this channel.

#### Returns
A new instance of this class.

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
* `startTime` The time from which to consider session history.
* `completionBlock` The code block to execute upon completion. This provides access to the activity history.

## Example
The following sample code shows how to initialize an MCDUserActivityChannel.

```ObjectiveC
// You must be logged in to use UserActivities
NSArray<MCDUserAccount*>* accounts = [[AppDataSource sharedInstance].accountProvider getUserAccounts];
if (accounts.count > 0)
{
    // Get a UserActivity channel, getting the default channel        
    NSLog(@"Creating UserActivityChannel");
    NSArray<MCDUserAccount*>* accounts = [[AppDataSource sharedInstance].accountProvider getUserAccounts];
    MCDUserDataFeed* userDataFeed = [MCDUserDataFeed userDataFeedForAccount:accounts[0]
        platform:[AppDataSource sharedInstance].platform
        activitySourceHost:CROSS_PLATFORM_APP_ID];
    NSArray<MCDSyncScope*>* syncScopes = @[ [MCDUserActivityChannel syncScope] ];
    [userDataFeed addSyncScopes:syncScopes];
    self.channel = [MCDUserActivityChannel userActivityChannelWithUserDataFeed:userDataFeed];
}
else
{
    NSLog(@"Must have an active account to publish activities!");
    self.createActivityStatusField.text = @"Need to be logged in!";
}
```