---
title: ApplicationRegistration
description: This class represents an application that is registered for remote connectivity.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# ApplicationRegistration class

```
public final class ApplicationRegistration implements IApplicationRegistration
```

This class represents an application that is registered for remote connectivity. A remote app can provide remote app services or be used to launch a URI.

## Methods

### getAttributes 
`public Map<String, String> getAttributes()`

Gets the attributes associated with this application.

#### Returns
A Map of key/value pairs defining the attributes of this registration.

### getAppServiceProviders
`public AppServiceProvider[] getAppServiceProviders()`

Gets the app service provider associated with this application.

#### Returns
An array of [AppServiceProvider](AppServiceProvider.md) instances.

### getLaunchUriProvider
`public LaunchUriProvider getLaunchUriProvider()`
Gets the URI launcher for this application.

#### Returns
A [LaunchUriProvider](LaunchUriProvider.md) instance.