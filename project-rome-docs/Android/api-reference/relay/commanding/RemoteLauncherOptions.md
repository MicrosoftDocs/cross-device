---
title: RemoteLauncherOptions class
description: This class specifies the options used to launch the default app for URI on a remote device.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteLauncherOptions class

```
public final class RemoteLauncherOptions
```

This class specifies the options used to launch the default app for URI on a remote device.


## Constructors

### RemoteLauncherOptions
`public RemoteLauncherOptions()`

Initialized an instance of this class with default values.

### RemoteLauncherOptions
`public RemoteLauncherOptions(@Nullable String fallbackUri, @Nullable String[] preferredPackageIds)`

Initializes an instance of the RemoteLauncherOptions class.

#### Parameters  
* `fallbackUri` The URI of the website to open in the event that the original URI cannot be handled by the intended app
* `preferredPackageIds` a list of package IDs of apps that should be used to launch the URI on the remote device. The first string on the list should correspond to the preferred application.  

## Methods

### getFallbackUri
`public String getFallbackUri()`

Returns the URI of the website to open in the event that the original URI cannot be handled by the intended app.

#### Returns
The fallback URI String.

### setFallbackUri
`public void setFallbackUri(@Nullable String fallbackUri)`

Sets the URI of the website to open in the event that the original URI cannot be handled by the intended app.

#### Parameters
* `fallbackUri` The fallback URI string.

### getPreferredPackageIds
`public String[] getPreferredPackageIds()`

Returns an array of package IDs of apps that should be used to launch the URI on the remote device.

#### Returns
The array of preferred app identifiers.

### setPreferredPackageIds
`public void setPreferredPackageIds(@Nullable String[] preferredPackageIds)`

Sets the apps that should be used to launch the URI on the remote device.

#### Parameters
* `preferredPackageIds` The package IDs of the preferred apps.

