---
title: MCDRemoteSystem
description: A class to represent a remote system.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystem` 

```
@interface MCDRemoteSystem : NSObject
```  

A class to represent a remote system.

## Properties

### kind
`@property(nonatomic, readonly, nonnull) NSString* kind;`

The device type of this remote system.

### systemId
`@property(nonatomic, readonly, nonnull) NSString* systemId;`

The identifier for this remote system.

### displayName
`@property(nonatomic, readonly, nonnull) NSString* displayName;`

The friendly display name of this remote system.

### status
`@property(nonatomic, readonly) MCDRemoteSystemStatus status;`

The availability status of the remote system.

### manufacturerDisplayName
`@property(nonatomic, readonly, nonnull) NSString* manufacturerDisplayName;`

The display name of the remote system manufacturer.

### modelDisplayName
`@property(nonatomic, readonly, nonnull) NSString* modelDisplayName;`

The display name of the remote system model.

### applications
`@property(nonatomic, readonly, nonnull) NSArray<MCDRemoteSystemApplication*>* applications;`

An array of the applications on this remote system that are available for connectivity.

### platform
`@property(nonatomic, readonly) MCDRemoteSystemPlatform platform;`

The MCDRemoteSystemPlatform managing remote system activity.

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