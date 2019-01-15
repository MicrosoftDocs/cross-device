---
title: include file
description: include file
ms.author: carmenf
author: CarmenForsmann
ms.date: 01/10/2019
ms.topic: include
ms.assetid: 
ms.localizationpriority: medium
---

### Prepare account that will be used by the platform

Purposeful why

snippet from the sample
​
after platform started is to invoke GetAllAccounts on AccountManager to get a list of accounts that previously been added into CDP AccountManager.

So App needs to make sure before Adding an account to AccoutManager, it shall remove any existing account from AccountManager. The SDK will throw InvalidState Exception if App tries to add an new account but AccountManager already contains one.

<should something go here about the auth provider?>

When App calls AccountManager::AddAcountAsync with a new account, AccountManager fires CCS tokenRequest in order to fetch other identity info for this account ​
App, subscribing to AccessTokenRequestedEvent, needs to respond to this event by either calling CompleteWithAccessToken with a token when app successfully retrieves the token from its token library, or by calling CompleteWithErrorMessage with an error message if App failed to fetch the token using its token library​
This is true for any other token request from by OneSDK, e.g., token requests for wns, ccs, dds etc.​

Pre 1.0
The **UserAccountProvider** is needed to deliver an OAuth 2.0 access token for the current user's access to the Connected Devices Platform. It will be called the first time the app is run and upon the expiration of a platform-managed refresh token. 

In order to help developers onboard with the platform more easily, we have provided account provider implementations for Android and iOS. These implementations, found in the [authentication provider sample](https://github.com/Microsoft/project-rome/tree/master/iOS/samples/account-provider-sample), can be used to obtain the OAuth 2.0 access token and refresh token for your app.

[!INCLUDE [auth-scopes](../auth-scopes.md)]

```ObjectiveC