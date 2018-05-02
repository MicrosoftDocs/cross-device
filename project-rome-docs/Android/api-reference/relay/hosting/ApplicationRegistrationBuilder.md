---
title: ApplicationRegistrationBuilder
description: A builder class for ApplicationRegistration instances.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# ApplicationRegistrationBuilder class

```
public final class ApplicationRegistrationBuilder
```

A builder class for [ApplicationRegistration](ApplicationRegistration.md) instances.

## Constructors

### ApplicationRegistrationBuilder
`public ApplicationRegistrationBuilder()`

Creates and initializes an instance of this class.

## Methods

### addAttribute
`public void addAttribute(@NonNull String name, @Nullable String value)`

Adds a key/value attribute to the application registration.

#### Parameters
* `value` The attribute value.
* `name` The name of the attribute.

### addAppServiceProvider
`public void addAppServiceProvider(@NonNull AppServiceProvider provider)`

Adds an app service provider to the application registration.

#### Parameters
* `provider` The [AppServiceProvider](AppServiceProvider.md) to add.

### setLaunchUriProvider
`public void setLaunchUriProvider(@NonNull LaunchUriProvider launchUriProvider)`

Sets the URI launcher for this application registration.

#### Parameters
* `launchUriProvider` The [LaunchUriProvider](LaunchUriProvider.md) that will handle URI launches for this application.


### buildRegistration
`public ApplicationRegistration buildRegistration()`

Builds an application registration with the specified properties.

#### Returns
A new [ApplicationRegistration](ApplicationRegistration.md) instance.