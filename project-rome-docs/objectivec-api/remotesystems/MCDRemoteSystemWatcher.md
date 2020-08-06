---
title: MCDRemoteSystemWatcher
description: Learn about the MCDRemoteSystemWatcher class and its properties. This class is used to discover remote systems.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemWatcher`

```
@interface MCDRemoteSystemWatcher : NSObject
```

A class used to discover remote systems. 

## Properties

### remoteSystemAdded
```
@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemAddedEventArgs*>* remoteSystemAdded;
```

Event for when a new remote system is discovered.

### remoteSystemUpdated
```
@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemUpdatedEventArgs*>* remoteSystemUpdated;
```

Event for when a remote system that was previously discovered in this discovery session changes from proximally
connected to cloud connected, or the reverse. 

### remoteSystemRemoved
```
@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*, MCDRemoteSystemRemovedEventArgs*>* remoteSystemRemoved;
```

Event for when a remote system is removed. 

### enumerationCompleted
```
@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*,  MCDRemoteSystemEnumerationCompletedEventArgs*>* enumerationCompleted;
```

Event for when the initial discovery of currently-discoverable devices has finished.  The discovery process will continue to run and will raise additional events if the set of existing remote systems changes.

### errorOccurred
```
@property(nonatomic, readonly, nonnull) MCDEvent<MCDRemoteSystemWatcher*,  MCDRemoteSystemWatcherErrorOccurredEventArgs*>* errorOccurred;
```

Event for when an error occurs during discovery. The discovery process will continue if possible. For example, if the error
occurs with a value of **MCDRemoteSystemWatcherError.MCDRemoteSystemWatcherErrorInternetNotAvailable**, proximal discovery
may continue because the error applies only to cloud discovery (see **MCDRemoteSystemDiscoveryType**).

## Constructors

### watcher
```
+ (nullable instancetype)watcher;
```

Creates and initializes a new instance of this class.

#### Returns 
Returns a new instance of this class.

### watcherWithFilters
```
+ (nullable instancetype)watcherWithFilters:(nonnull NSArray<NSObject<MCDRemoteSystemFilter>*>*)filters;
```

Creates and initializes a new instance of this class with filters.

#### Parameters 
* `filters` 

An array of filters to use in the device discovery process.

#### Returns 
Returns an MCDRemoteSystemWatcher object with filters.

### initWithFilters
```
- (nullable instancetype)initWithFilters:(nonnull NSArray<NSObject<MCDRemoteSystemFilter>*>*)filters;
```

Creates and initializes a new instance of this class with filters.

#### Parameters 
* `filters` 

An array of filters to use in the device discovery process.

#### Returns 
Returns an MCDRemoteSystemWatcher object initialized with filters.

## Methods

### start
`- (void)start;`

Begins discovering remote systems.

### stop
`- (void)stop;` 

Stops the active discovery.
