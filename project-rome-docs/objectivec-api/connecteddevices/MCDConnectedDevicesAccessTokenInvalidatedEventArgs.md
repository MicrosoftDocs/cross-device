---
title: MCDConnectedDevicesAccessTokenInvalidatedEventArgs
description: Inform that token associated with ConnectedDevicesAccount reported a token error.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesAccessTokenInvalidatedEventArgs` 

```
@interface MCDConnectedDevicesAccessTokenInvalidatedEventArgs : NSObject 
```  
Returned by MCDConnectedDevicesAccount to inform that the token associated with MCDConnectedDevicesAccount reported
token error for the contained scopes. Token provider needs to either refresh their token cache or potentially pop up
UI to ask user to sign in in order to fix their account setup.

## Properties

### account
`@property (nonatomic, readonly, nonnull) MCDConnectedDevicesAccount* account;`

The Account associated with this MCDConnectedDevicesAccessTokenInvalidatedEventArgs.

### scopes
`@property (nonatomic, readonly, nonnull) NSArray<NSString*>* scopes;`

The list of scopes for which the token must cover when generated.