---
title: MCDUserNotificationReader
description: This class is used to get the results of a notification query.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationReader`

```
@interface MCDUserNotificationReader : NSObject
```

This class is used to get the results of a notification query.

## Methods

// @brief Used to get the next batch of notifications from the current query, up to the limit set the by the caller. Set the limit to 0
// to get all the rest of notifications.
### readBatchAsyncWithMaxSize
`- (void)readBatchAsyncWithMaxSize:(NSUInteger)maxBatchSize
                       completion:(nonnull void (^)(NSArray<MCDUserNotification*>* _Nullable, NSError* _Nullable))completion;`

Gets the user notifications, up to the given batch size.

#### Parameters
* `maxBatchSize` The maximum number of notifications to get. A value of 0 gets all available notifications.
* `completion` The code block to execute upon completion. This contains the array of retrieved notifications.