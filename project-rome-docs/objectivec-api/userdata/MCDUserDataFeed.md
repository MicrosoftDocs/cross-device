---
title: MCDUserDataFeed
description: This class is responsible for synchronizing user-specific data with the Connected Devices Platform backend.
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserDataFeed`

```
@interface MCDUserDataFeed : NSObject
```

This class is responsible for synchronizing user-specific data with the Connected Devices Platform backend. The data that is synchronized depends on which **[MCDUserDataFeedSyncScope](MCDUserDataFeedSyncScope.md)** instances are contained.

## Properties

### syncStatus
`@property(nonatomic, readonly) MCDUserDataSyncStatus syncStatus;`

Describes the current status of user data synchronization.

### syncStatusChanged
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDUserDataFeed*, MCDUserDataFeedSyncStatusChangedEventArgs*>* syncStatusChanged;`

Event for when the sync status of the UserDataFeed changes.

## Constructors

### getForAccount
`+ (nullable instancetype)getForAccount:(nonnull MCDConnectedDevicesAccount*)userAccount
                                   platform:(nonnull MCDConnectedDevicesPlatform*)platform
                         activitySourceHost:(nonnull NSString*)activitySourceHost;`

Creates and initializes a new instance of this class with a user account, platform instance, and the cross-platform app ID.

#### Parameters
* `userAccount` 

The user account that this data will be associated with.

* `platform` 

The **MCDPlatform** instance that has been initialized for this app's Connected Devices functionality.

* `activitySourceHost` 

The cross-platform app ID. This is retrieved through the Microsoft Developer Dashboard registration.

#### Returns
Returns an instance of this class.

## Methods

### subscribeToSyncScopesAsync
`- (void)subscribeToSyncScopesAsync:(NSArray<id<MCDUserDataFeedSyncScope>>* _Nonnull) syncScopes callback:(nonnull void (^)(BOOL, NSError* _Nullable)) callback;`

Adds **MCDUserDataFeedSyncScope** instances to this MCDUserDataFeed.  This MCDUserDataFeed is synchronized according to the **MCDUserDataFeedSyncScope** instances specified.

#### Parameters

* `syncScopes`
An array of **MCDSyncScope** instances.

* `callback`

The callback result indicates if subscription is successful, or not. 

### startSync
`- (void)startSync;`

Starts the synchronization process with the Connected Devices Platform. During this operation, the **syncStatus** property will be updated and change events will be raised.