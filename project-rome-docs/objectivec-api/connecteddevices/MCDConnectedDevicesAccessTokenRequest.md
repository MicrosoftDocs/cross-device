---
title: MCDConnectedDevicesAccessTokenRequest
description: Request for an access token for the contained MCDConnectedDevicesAccount which satisfies the contained scopes.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesAccessTokenRequest` 

```
@interface MCDConnectedDevicesAccessTokenRequest : NSObject
```  
Request for an access token for the contained MCDConnectedDevicesAccount which satisfies the contained scopes.

## Properties

### account
`@property (nonatomic, readonly, nonnull) MCDConnectedDevicesAccount* account;`

The Account associated with this MCDConnectedDevicesAccessTokenInvalidatedEventArgs.

### scopes
`@property (nonatomic, readonly, nonnull) NSArray<NSString*>* scopes;`

The list of scopes for which the token must cover when generated.

## Methods

### completeWithAccessToken
`- (void) completeWithAccessToken:(NSString* _Nonnull) token;`

If a token with the requested scopes was successfully generated, call this method with the token to complete the request.

#### Parameters 
* `token` 

Successfully generated token

### completeWithErrorMessage
`- (void) completeWithErrorMessage:(NSString* _Nullable) errorMessage;`

If a token with the requested scopes was not successfully generated for any reason, call this method with a message to be used for logging.

#### Parameters 
* `errorMessage`

A message describing why the token was unsuccessful.