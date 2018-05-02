---
title: AccessTokenResult 
description: This class represents the result of the app fetching an access token.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# AccessTokenResult class

```
public final class AccessTokenResult
```

This class represents the result of the app fetching an access token. It is provided by the developer and received by the Connected Devices Platform.

## Constructors

### AccessTokenResult
`public AccessTokenResult(@NonNull AccessTokenRequestStatus status, @NonNull String accessToken)`  

Initializes an instance of the AccessTokenResult class with a result status and a token string.

#### Parameters  
* `status` The status of the token retrieval operation.
* `accessToken` The access token String.

## Methods

### getTokenRequestStatus
`public AccessTokenRequestStatus getTokenRequestStatus()` 

Gets the token request status.

#### Returns
An [AccessTokenRequestStatus](AccessTokenRequestStatus.md) value corresponding to the status.

### getAccessToken
`public String getAccessToken()`

Gets the access token used to construct the result class. This will only be called by the system if **getTokenRequestStatus** indicates a successful token retrieval.

#### Returns
The access token String.

## Example

The following sample code requests an MSA access token and uses an AccessTokenResult to handle the response.

```Java
/**
* Asynchronously requests a new access token for the provided scope(s) and caches it.
* This assumes that the sign in helper is currently signed in.
*/
private AsyncOperation<AccessTokenResult> requestNewAccessTokenAsync(final String scope) {
// Need the refresh token first, then can use it to request an access token
return mTokenCache.getRefreshTokenAsync()
    .thenComposeAsync(new AsyncOperation.ResultFunction<String, AsyncOperation<MSATokenRequest.Result>>() {
        @Override
        public AsyncOperation<MSATokenRequest.Result> apply(String refreshToken) {
            return MSATokenRequest.requestAsync(mClientId, MSATokenRequest.GrantType.REFRESH, scope, null, refreshToken);
        }
    })
    .thenApplyAsync(new AsyncOperation.ResultFunction<MSATokenRequest.Result, AccessTokenResult>() {
        @Override
        public AccessTokenResult apply(MSATokenRequest.Result result) throws Throwable {
            switch (result.getStatus()) {
            case SUCCESS:
                Log.i(TAG, "Successfully fetched access token.");
                mTokenCache.setAccessToken(result.getAccessToken(), scope, result.getExpiresIn());
                return new AccessTokenResult(AccessTokenRequestStatus.SUCCESS, result.getAccessToken());

            case TRANSIENT_FAILURE:
                Log.e(TAG, "Requesting new access token failed temporarily, please try again.");
                return new AccessTokenResult(AccessTokenRequestStatus.TRANSIENT_ERROR, null);

            default: // PERMANENT_FAILURE
                Log.e(TAG, "Permanent error occurred while fetching access token.");
                onAccessTokenError(mAccount.getId(), new String[] { scope }, true);
                throw new IOException("Permanent error occurred while fetching access token.");
            }
        }
    });
}
```