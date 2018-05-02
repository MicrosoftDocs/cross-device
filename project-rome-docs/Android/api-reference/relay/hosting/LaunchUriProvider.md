---
title: LaunchUriProvider
description: This interface provides methods for handling a URI sent through the Connected Devices Platform.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# LaunchUriProvider interface

```
public interface LaunchUriProvider
```

This interface provides methods for handling a URI sent through the Connected Devices Platform. An application must implement this interface in order to respond to URI launch requests.

## Methods

### onLaunchUriAsync
`@NonNull AsyncOperation<Boolean> onLaunchUriAsync(@NonNull String uri, @Nullable String fallbackUri, @Nullable String[] preferredPackageIds);`

This method is called when a remote device attempts to launch a URI on this device.

#### Parameters 
* `uri` The URI to launch.
* `fallbackUri` The web-friendly URI to launch in the event that the primary URI fails.
* `preferredPackageIds` The list of IDs of preferred applications to handle this URI.

#### Returns
An asynchronous operation with a Boolean value: true if the URI launched successfully, otherwise false.

### getSupportedUriSchemes
`@Nullable String[] getSupportedUriSchemes();`

This method is called to determine whether the application can handle a given URI. The application must define which URI schemes it supports.

#### Returns
An array of strings representing the supported URI schemes.