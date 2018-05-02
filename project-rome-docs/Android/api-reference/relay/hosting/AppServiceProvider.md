---
title: AppServiceProvider 
description: This interface contains methods for making a local app service accessible to remote devices.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# AppServiceProvider interface

```
public interface AppServiceProvider
```

This interface contains methods for making a local app service accessible to remote devices. Developers must implement this interface to make their app services available for remote connectivity.

## Methods

### onConnectionOpened
`void onConnectionOpened(AppServiceConnection connection)` 

This method is called by the platform when a remote device opens a connection to a local app service.

#### Parameters
* `connection` The [AppServiceConnection](AppServiceConnection.md) instance corresponding to the connection to a remote app service that was opened. This instance is needed for remote messaging with the app service.

### getAppServiceDescription
`@NonNull AppServiceDescription getAppServiceDescription();` 

This method provides a description (containing the name string) of the app service.

#### Returns
An [AppServiceDescription](AppServiceDescription.md) instance.