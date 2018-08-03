---
title: MCDUserDataFeed
description: This class is responsible for synchronizing user-specific data with the Connected Devices Platform backend.
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserDataFeed`

```
@interface MCDUserDataFeed : NSObject
```

This class is responsible for synchronizing user-specific data with the Connected Devices Platform backend. The data that is synchronized depends on which **[MCDSyncScope](MCDSyncScope.md)** instances are contained.

## Constructors

### userDataFeedForAccount
`+ (nullable instancetype)userDataFeedForAccount:(nonnull MCDUserAccount*)userAccount
                                   platform:(nonnull MCDPlatform*)platform
                         activitySourceHost:(nonnull NSString*)activitySourceHost;`

Creates and initializes a new instance of this class with a user account, platform instance, and the cross-platform app ID.

#### Parameters
* `userAccount` The user accound that this data will be associated with.
* `platform` The **MCDPlatform** instance that has been initialized for this app's Connected Devices functionality.
* `activitySourceHost` The cross-platform app ID. This is retrieved through the Microsoft Developer Dashboard registration (see [Hosting cross-device experiences (iOS)](../../hosting/ios/how-to-guides/hosting-ios.md)).


#### Returns
An instance of this class.

## Properties

### syncStatus
`@property(nonatomic, readonly) MCDUserDataSyncStatus syncStatus;`

Describes the status of user data synchronization.


## Methods

### addSyncScopes
`- (void)addSyncScopes:(nonnull NSArray<MCDSyncScope*>*)syncScopes;`

Adds **MCDSyncScope** instances to this data feed. **MCDSyncScope**s define which data needs to by synchronized with the Connected Devices Platform.

#### Parameters
* `syncScopes` An array of **MCDSyncScope** instances.

### addSyncStatusChangedListener
`- (NSUInteger)addSyncStatusChangedListener:(nonnull void (^)(MCDUserDataFeed* _Nonnull))listener;`

Adds an event listener for the "sync status changed" event.

#### Parameters
* `listener` The event listener.

#### Returns
An event registration token (required to remove this registration).

### removeSyncStatusChangedListener
`- (void)removeSyncStatusChangedListener:(NSUInteger)eventRegistrationToken;`

Removes an event listener for the "sync status changed" event.

#### Parameters
`eventRegistrationToken` The unique registration ID for the event listener to be removed.

### startSync
`- (void)startSync;`

Starts the synchronization process with the Connected Devices Platform. During this operation, the **syncStatus** property will be updated and change events will be raised.

