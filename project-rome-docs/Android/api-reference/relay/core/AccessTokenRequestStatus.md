---
title: AccessTokenRequestStatus 
description: Contains the values that describe the status of an access token request.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# AccessTokenRequestStatus enum
Contains the values that describe the status of an access token request.

## Fields

|Name   |Value   |Description   |
|:--------|:-------|:-------------|
|SUCCESS|0|The token was retrieved successfully.|
|TRANSIENT_ERROR|1|There was an error retrieving the token. If the Connected Devices Platform receives this value in an [AccessTokenResult](AccessTokenResult.md), it will try again after a delay.|
