---
title: MCDAccessTokenRequestStatus
description: Contains values that describe the status of an access token request.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# enum `MCDAccessTokenRequestStatus`

```
typedef NS_ENUM(NSInteger, MCDAccessTokenRequestStatus)
```

Contains values that describe the status of an access token request.

|Name | Value | Description |
|:-- |:-- |:-- |
|MCDAccessTokenRequestStatusSuccess|0|The token was retrieved.|
|MCDAccessTokenRequestStatusTransientError|1| There was an error retrieving the token. If the Connected Devices Platform receives this value in an [MCDAccessTokenResult](MCDAccessTokenResult.md), it will try again after a delay.|
