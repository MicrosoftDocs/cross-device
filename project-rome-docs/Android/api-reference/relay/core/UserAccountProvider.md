---
title: UserAccountProvider
description: This interface must be implemented by an app in order to provide access to the user account.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserAccountProvider interface

```
public interface UserAccountProvider
```

This interface must be implemented by an app in order to provide access to the user account.


## Methods

### getUserAccounts
`@Nullable UserAccount[] getUserAccounts();`

This method gets the current snapshot of user accounts on the application.

#### Returns
An array of [UserAccount](UserAccount.md) instances.

### getAccessTokenForUserAccountAsync
`@NonNull AsyncOperation<AccessTokenResult> getAccessTokenForUserAccountAsync(@NonNull String userAccountId, @NonNull String[] scopes);`

This method gets an access token for a given user account.

#### Parameters
* `userAccountId` The identifier of the user account.
* `scopes` The scopes of the access token.

#### Returns
An asynchronous operation with the access token result.

### addUserAccountChangedListener
`long addUserAccountChangedListener(@NonNull EventListener<UserAccountProvider, Void> listener);`

This method associates an event listener with the event in which the signed-in user account changes.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
A unique identifier for this event registration (this is needed to remove the listener).

### removeUserAccountChangedListener
`void removeUserAccountChangedListener(long id);`

This method removes an event listener from the event in which the signed-in user account changes.

#### Parameters
* `id` The unique identifier for the original event registration.

### onAccessTokenError
`void onAccessTokenError(@NonNull String userAccountId, @NonNull String[] scopes, boolean isPermanentError);`

This method is called if there is an error using the access token. 

#### Parameters
* `userAccountId` The identifier of the user account.
* `scopes` The scopes of the access token.
* `isPermanentError` equals true if the error requires the user to sign in again, false if the issue can be resolved by refreshing the token.

## Example

The MSAAccountProvider class in the sample app implements this interface.