---
title: MCDAccessTokenResult
description: This class represents the result of the app fetching an access token.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDAccessTokenResult`

```
@interface MCDAccessTokenResult : NSObject 
```

This class represents the result of the app fetching an access token. It is provided by the developer and received by the Connected Devices Platform.

## Properties

### tokenRequestStatus
`@property(nonatomic, readonly) MCDAccessTokenRequestStatus tokenRequestStatus;`

The status of the access token request.

### accessToken
`@property(nonatomic, readonly, copy, nonnull) NSString* accessToken;`

The access token string used to construct the result class. This will only be queried by the system if the status field indicates a successful token retrieval.

## Constructors

### resultWithAccessToken
`+ (nullable instancetype)resultWithAccessToken:(nullable NSString*)accessToken status:(MCDAccessTokenRequestStatus)status;` 

Creates a new instance of this class with an access token and a descriptive status value.

#### Parameters
* `accessToken` The access token.  
* `status` The status of the token retrieval operation.

#### Returns
A new instance of this class.

### initWithAccessToken
`- (nullable instancetype)initWithAccessToken:(nullable NSString*)accessToken status:(MCDAccessTokenRequestStatus)status;`

Creates a new instance of this class with an access token and a descriptive status value.

#### Parameters
* `accessToken` The access token.  
* `status` The token request status.

#### Returns
A new instance of this class.