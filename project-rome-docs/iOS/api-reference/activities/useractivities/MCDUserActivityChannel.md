---
title: MCDUserActivityChannel
description: This class handles the adding and querying of user activities for the application.
keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
---

# class `MCDUserActivityChannel`

```
@interface MCDUserActivityChannel : NSObject
```

This class handles the adding and querying of user activities for the application.

## Properties

## Constructors

### userActivityChannelWithUserAccount
`+ (nullable instancetype)userActivityChannelWithUserAccount:(nonnull MCDUserAccount*)userAccount
                                         activitySourceHost:(nullable NSString*)activitySourceHost;`

#### Parameters
* `userAccount` The user account associated with the activities on this channel.
* `activitySourceHost` [optional] A string indicating the source of the activities on this channel.

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
The following sample code show how to create a MCDUserActivityChannel.

```Objective-C
// An account provider is needed for this step.
static id<MCDUserAccountProvider> s_accountProvider;

@implementation UserActivityViewController

// When the current view loads (or at any designated point in the application),
// get a User Activity channel.
- (void)viewDidLoad {
    [super viewDidLoad];
    
    // You must be logged in to use UserActivities. IdentityViewController is defined
    // elsewhere in the sample app.
    s_accountProvider = [IdentityViewController accountProvider];
    NSArray<MCDUserAccount*>* accounts = [s_accountProvider getUserAccounts];
    if (accounts.count > 0)
    {
        // Get a UserActivity channel for the default account
        self.channel = [MCDUserActivityChannel userActivityChannelWithUserAccount:accounts[0]];
    }
    else
    {
        // notify user that they must log in to use Activities
        NSLog(@"Must have an active account to publish activities!");
        self.createActivityStatusField.text = @"Need to be logged in!";
    }
}
```