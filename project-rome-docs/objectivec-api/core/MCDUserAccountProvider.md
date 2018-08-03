---
title: MCDUserAccountProvider
description: This protocol must be implemented by an app in order to provide an access token for a user account.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# protocol `MCDUserAccountProvider`

```
@protocol MCDUserAccountProvider<NSObject>
```

This protocol must be implemented by an app in order to provide an access token for a user account.


## Properties

### userAccountChanged
`@property(nonatomic, readonly, strong, nonnull) MCDUserAccountChangedEvent* userAccountChanged;`

An event that will be listened to by the connected devices platform. This event should be raised whenever a user account is changed (added, removed, interrupted, fixed). It should be initialized in the implementing class' initializer.


## Methods

### getAccessTokenForUserAccountIdAsync
`- (void)getAccessTokenForUserAccountIdAsync: (nonnull NSString*)accountId 
                                     scopes: (nonnull NSArray<NSString*>*)scopes 
                                 completion: (nonnull void (^)(MCDAccessTokenResult* _Nullable, NSError* _Nullable))completionBlock;`

Gets the access token for a user account.

#### Parameters
* `accountId` The identifier of the user account.
* `scopes` The scopes of the access token. The first element is expected to contain all of the scopes required by the Connected Devices Platform, each separated by whitespace.
* `completionBlock` The code block to execute upon completion. This provides access to the token result.

### getUserAccounts
`- (nonnull NSArray<MCDUserAccount*>*)getUserAccounts;`

Fetches the current snapshot of user accounts.

#### Returns
An array of user accounts.

### onAccessTokenError
`- (void)onAccessTokenError:(nonnull NSString*)accountId scopes:(nonnull NSArray<NSString*>*)scopes isPermanentError:(BOOL)isPermanentError;`

This method is called if there is an error using the access token.

#### Parameters
* `accountId` The identifier of the user account.
* `scopes` The scopes of the access token.
* `isPermanentError` equals YES if the error requires the user to sign in again, NO if the issue can be resolved by refreshing the token.

