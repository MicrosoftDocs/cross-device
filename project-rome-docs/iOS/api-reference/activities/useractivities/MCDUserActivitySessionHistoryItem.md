---
title: MCDUserActivitySessionHistoryItem
description: This class provides the start and end time that a user was engaged in a particular activity.
keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
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

## Example
The following sample code shows how to use MCDUserActivitySessionHistoryItem instances to fetch and read the user's User Activities in your app.

```Objective-C
// In the context of the sample app, this method is called on a button click
- (IBAction)readActivityButton:(id)sender {
    
    // Read/sync your UserActivities
    [self.channel getRecentUserActivitiesAsync:(NSInteger)5
        // handle the method completion (parse the activity item):
        completion:^(NSArray<MCDUserActivitySessionHistoryItem*>* _Nonnull result, NSError* _Nullable error) {
            dispatch_async(dispatch_get_main_queue(), ^{
                if (error) {
                    // handle the retrieval error
                }
                else if (result.count == 0) {
                    // report that no activities were found
                }
                else {
                    // reference the first activity on the list
                    // (for example)
                    MCDUserActivitySessionHistoryItem* item = result.firstObject;
                    // write the activity data in program memory/UI
                    self.activityList.text = item.userActivity.activityId;
                    self.activityDisplay.text = item.userActivity.visualElements.displayText;
                }
            });
        }];
}
```
