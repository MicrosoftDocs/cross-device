---
title: UserAccount
description: This class represents a single user account known by an app.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# UserAccount class

```
public final class UserAccount
```

This class represents a single user account known by an app.

## Constructors

### UserAccount
`public UserAccount(@NonNull String id, @NonNull UserAccountType type)`

Creates and initializes a new instance of this class with an ID string and account type definition.

#### Parameters
* `id` A unique identifier string for this user account.
* `type` The [UserAccountType](UserAccountType.md) of the account (depends on which ID provider the account is from).

## Methods

### getId
`public String getId()`

Gets the unique identifier for this user account.

#### Returns
The unique identifier String for this user account.

### getType
`public UserAccountType getType()`

Gets the type of account.

#### Returns 
A [UserAccountType](UserAccountType.md) value describing the type of account.

## Example

The following code constructs an instance of MSAAccountProvider, which is a sample class that implements the UserAccountProvider interface. It creates a UserAccount member in its constructor.

```Java
// region Constructor
/**
* @param clientId              id of the app's registration in the MSA portal
* @param context
*/
public MSAAccountProvider(String clientId, Context context) {
    mClientId = clientId;
    mTokenCache = new MSATokenCache(clientId, context);
    mTokenCache.addListener(new MSATokenCache.Listener() {
        @Override
        public void onTokenCachePermanentFailure() {
            onAccessTokenError((mAccount != null ? mAccount.getId() : null), null, true);
        }
    });

    if (mTokenCache.loadSavedRefreshToken()) {
        Log.i(TAG, "Loaded previous session for MSAAccountProvider. Starting as signed in.");
        mAccount = new UserAccount(UUID.randomUUID().toString(), UserAccountType.MSA);
    } else {
        Log.i(TAG, "No previous session could be loaded for MSAAccountProvider. Starting as signed out.");
    }
}
```