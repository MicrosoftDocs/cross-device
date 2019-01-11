---
title: MCDRemoteSystemWatcher
description: A class used to discover remote systems.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemWatcher`

```
@interface MCDRemoteSystemWatcher : NSObject
```

A class used to discover remote systems. 

## Properties

### remoteSystemAdded
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemAddedEventArgs*>* remoteSystemAdded;`

TODO

### remoteSystemUpdated
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemUpdatedEventArgs*>* remoteSystemUpdated;`

TODO

### remoteSystemRemoved
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemRemovedEventArgs*>* remoteSystemRemoved;`

TODO

### enumerationCompleted
`@property(nonatomic, readonly, nonnull)
    MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemEnumerationCompletedEventArgs*>* enumerationCompleted;`

TODO

### errorOccurred
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemWatcherErrorOccurredEventArgs*>* errorOccurred;`

TODO

## Constructors

### watcher
`+ (nullable instancetype)watcher;`

#### Returns 
A new instance of this class.

### watcherWithFilters
`+ (nullable instancetype)watcherWithFilters:(nonnull NSArray<NSObject<MCDRemoteSystemFilter>*>*)filters;`

#### Parameters 
* `filters` An array of filters to use in the device discovery process.

#### Returns 
A new instance of this class with the given discovery filters applied.

### initWithFilters
`- (nullable instancetype)initWithFilters:(nonnull NSArray<NSObject<MCDRemoteSystemFilter>*>*)filters;`

#### Parameters 
* `filters` An array of filters to use in the device discovery process.

#### Returns 
A new instance of this class with the given discovery filters applied.

## Methods

### start
`- (void)start;`

Begins discovering remote systems.

### stop
`- (void)stop;` 

Stops the active discovery.