---
title: MCDUserNotificationReader
description: This class is used to get the results of a notification query.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationReader`

```
@interface MCDUserNotificationReader : NSObject
```

This class provides new incoming user notifications and user notification updates. It also provides access to the collection of user notifications persisted in the Connected Device Platform. 	


## Methods

### readBatchAsyncWithMaxSize
`- (void)readBatchAsyncWithMaxSize:(NSUInteger)maxBatchSize
                       completion:(nonnull void (^)(NSArray<MCDUserNotification*>* _Nullable, NSError* _Nullable))completion;`

Read notification changes including new incoming notifications and updates on existing notifications in batch.

### addDataChangedListener
`(nonnull void (^)(MCDUserNotificationReader* _Nonnull))listener`

Add a data change listener that gets triggered when there is incoming notifications or notification updates. 

### removeDataChangedListener
`(NSUInteger)eventRegistrationToken`

Add a data change listener that gets triggered when there is incoming notifications or notification updates. 

Remove the data change listener. 