---
title: MCDConnectedDevicesAccountManager
description: Provides a single entrypoint for all account-related features in the SDK.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesAccountManager` 

```
@interface MCDConnectedDevicesAccountManager : NSObject
```  
Provides a single entrypoint for all account-related features in the SDK.

## Properties

### accessTokenRequested
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDConnectedDevicesAccountManager*, MCDConnectedDevicesAccessTokenRequestedEventArgs*>* accessTokenRequested;`

This event is fired when there is a need to request a token. This event should be subscribed and ready to respond before any request is sent out.

### accessTokenInvalidated
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDConnectedDevicesAccountManager*, MCDConnectedDevicesAccessTokenInvalidatedEventArgs*>* accessTokenInvalidated;`

This event is fired when a token consumer reports a token error. The token provider needs to either refresh their token cache or request a new user login to fix their account setup.

### allAccounts
`@property (nonatomic, readonly, nonnull) NSArray<MCDConnectedDevicesAccount*>* allAccounts;`

All MCDConnectedDevicesAccount which are currently tracked by this manager.

## Methods

### addAccountAsync
`- (void) addAccountAsync:(MCDConnectedDevicesAccount* _Nonnull)account callback:(nonnull void (^)(MCDConnectedDevicesAddAccountResult* _Nonnull, NSError* _Nullable))callback;`

Add an account to account manager, callback will be invoked when it completes.

#### Parameters 
* `callback`

The callback result indicates if Account addition is successful or not. 

### removeAccountAsync
`- (void) removeAccountAsync:(MCDConnectedDevicesAccount* _Nonnull)account callback:(nonnull void (^)(MCDConnectedDevicesRemoveAccountResult* _Nonnull, NSError* _Nullable))callback;`

Remove an account to account manager, callback will be invoked when it completes.

#### Parameters 
* `callback` 

 The callback result indicates if Account removal is successful or not. 