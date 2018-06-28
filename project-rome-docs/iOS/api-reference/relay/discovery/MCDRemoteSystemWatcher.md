---
title: MCDRemoteSystemWatcher
description: A class used to discover remote systems.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemWatcher`

```
@interface MCDRemoteSystemWatcher : NSObject
```

A class used to discover remote systems. 

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

### addRemoteSystemAddedListener
`- (NSUInteger)addRemoteSystemAddedListener:(nonnull void (^)(MCDRemoteSystemWatcher* _Nonnull, MCDRemoteSystem* _Nonnull))listener;`

Adds a listener for the "remote system added" event.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeRemoteSystemAddedListener
`- (void)removeRemoteSystemAddedListener:(NSUInteger)eventRegistrationToken;`

Removes a listener from the "remote system added" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addRemoteSystemUpdatedListener
`- (NSUInteger)addRemoteSystemUpdatedListener:(nonnull void (^)(MCDRemoteSystemWatcher* _Nonnull, MCDRemoteSystem* _Nonnull))listener;`

Adds a listener for the "remote system updated" event.

>**Note:** This event is raised when a remote system (device) that was previously discovered in this discovery session changes from proximally connected to cloud connected, or the reverse. It is also raised when a remote system changes one of its monitored properties (see the properties of the **MCDRemoteSystem** class).

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeRemoteSystemUpdatedListener
`- (void)removeRemoteSystemUpdatedListener:(NSUInteger)eventRegistrationToken;`

Removes a listener from the "remote system updated" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addRemoteSystemRemovedListener
`- (NSUInteger)addRemoteSystemRemovedListener:(nonnull void (^)(MCDRemoteSystemWatcher* _Nonnull, MCDRemoteSystem* _Nonnull))listener;`

Adds a listener for the "remote system removed" event.

> **Note:** The "remote system removed" event is raised only after a RemoteSystem has stopped being discoverable over all of the categories specified by the associated **MCDRemoteSystemDiscoveryTypeFilter**.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeRemoteSystemRemovedListener
`- (void)removeRemoteSystemRemovedListener:(NSUInteger)eventRegistrationToken;`

Removes a listener from the "remote system removed" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addEnumerationCompletedListener 
`- (NSUInteger)addEnumerationCompletedListener:(nonnull void (^)(MCDRemoteSystemWatcher* _Nonnull))listener;`

Adds a listener for the "enumeration completed" event.

> The "enumeration completed" event is raised for different criteria depending on the discovery type(s), but in every case it is meant to signify the time when all available devices can be expected to have been discovered.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeEnumerationCompletedListener
`- (void)removeEnumerationCompletedListener:(NSUInteger)eventRegistrationToken;`

Removes a listener from the "enumeration completed" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addErrorOccurredListener
`- (NSUInteger)addErrorOccurredListener:(nonnull void (^)(MCDRemoteSystemWatcher* _Nonnull, MCDRemoteSystemWatcherError))listener;`

Adds a listener for the "error occurred" event.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeErrorOccurredListener
`- (void)removeErrorOccurredListener:(NSUInteger)eventRegistrationToken;`

Removes a listener from the "error occurred" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

## Example
The following sample code shows how to create and start a simple MCDRemoteSystemWatcher to discover RemoteSystem instances.

```ObjectiveC
// Create a RemoteSystemWatcher to discover devices
MCDRemoteSystemWatcher* _watcher;

-(void)startDiscovery {
    
    // create an array of empty filters
    NSMutableArray<NSObject<MCDRemoteSystemFilter>*>* filters = [[NSMutableArray alloc] init];

    // Start the watcher (method defined below)
    [self startWatcherWithFilter:filters];
    
}

// Start watcher with filter for transport types, form factors
- (void)startWatcherWithFilter:(NSMutableArray<NSObject<MCDRemoteSystemFilter>*>*)remoteSystemFilter {
    // set up basic tracking of discovery events
    _discoveredSystems = [[NSMutableArray alloc] init];
    _devicesAdded = 0;
    _devicesUpdated = 0;
    _devicesRemoved = 0;
    
    _watcher = (remoteSystemFilter.count > 0) ? [[MCDRemoteSystemWatcher alloc] initWithFilters:remoteSystemFilter] :
    [[MCDRemoteSystemWatcher alloc] init];
    
    RemoteSystemViewController* __weak weakSelf = self;
    // listeners for discovery events are defined below
    [_watcher addRemoteSystemAddedListener:^(
                                             __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemAdded:system]; }];
    
    [_watcher addRemoteSystemUpdatedListener:^(
                                               __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemUpdated:system]; }];
    
    [_watcher addRemoteSystemRemovedListener:^(
                                               __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemRemoved:system]; }];
    [_watcher start];
}

// define the event listeners:
// Handle when RemoteSystems are added
- (void)_onRemoteSystemAdded:(MCDRemoteSystem*)system {
    @synchronized(self) {
        _devicesAdded++;
        // keep a reference to the discovered remote system
        [_discoveredSystems addObject:system];
        [_delegate remoteSystemsDidUpdate];
    }
}

// Handle when RemoteSystems are updated
- (void)_onRemoteSystemUpdated:(MCDRemoteSystem*)system {
    @synchronized(self) {
        _devicesUpdated++;
        
        for (unsigned i = 0; i < _discoveredSystems.count; i++) {
            MCDRemoteSystem* cachedSystem = [_discoveredSystems objectAtIndex:i];
            if ([cachedSystem.displayName isEqualToString:system.displayName]) {
                [_discoveredSystems replaceObjectAtIndex:i withObject:system];
                break;
            }
        }
        [_delegate remoteSystemsDidUpdate];
    }
}

// Handle when RemoteSystems are removed
- (void)_onRemoteSystemRemoved:(MCDRemoteSystem*)system {
    @synchronized(self) {
        _devicesRemoved++;
        
        for (unsigned i = 0; i < _discoveredSystems.count; i++) {
            MCDRemoteSystem* cachedSystem = [_discoveredSystems objectAtIndex:i];
            if ([cachedSystem.displayName isEqualToString:system.displayName]) {
                [_discoveredSystems removeObjectAtIndex:i];
                break;
            }
        }
        [_delegate remoteSystemsDidUpdate];
    }
}
```