---
title: MCDUserNotificationChangeReader
description: TBD
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserNotificationChangeReader`

```
@interface MCDUserNotificationChangeReader : NSObject
```

TBD

## Properties

### serializedState
`@property(nonatomic, readonly, nonnull) NSString* serializedState;`

The current state of the change reader. This can be used to construct a new reader starting from the same state (based upon the last completed batch of notification changes, or the initial state if none have completed successfully).

## Methods

### readBatchAsyncWithMaxSize
`- (void)readBatchAsyncWithMaxSize:(NSUInteger)maxBatchSize
                       completion:(nonnull void (^)(NSArray<MCDUserNotificationChange*>* _Nullable, NSError* _Nullable))completion;`

Gets the next batch of notifications from the current query, up to the limit set by the caller.

#### Parameters
* `maxBatchSize` The maximum number of notifications to get. A value of 0 gets all available notifications.
* `completion` The code block to execute upon completion.