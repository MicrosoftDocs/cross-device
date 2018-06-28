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

Adds a key/value attribute to the application registration. For example, your app could define a unique ID attribute and share it with client devices. Then they can look for it in subsequent discoveries.

You can change your app's registered attributes by rebuilding an **ApplicationRegistration** with new attributes and re-initializing the Connected Devices Platform, but it is recommended that you keep your attributes constant, possibly adding more as needed when you update your app.

#### Parameters
* `value` The attribute value.
* `name` The name of the attribute.


### buildRegistration
`public ApplicationRegistration buildRegistration()`

Builds an application registration with the specified properties.

#### Returns
A new [ApplicationRegistration](ApplicationRegistration.md) instance.

## Example

The following sample code uses an ApplicationRegistrationBuilder to create an ApplicationRegistration instance. 

```Java
ApplicationRegistrationBuilder registrationBuilder = new ApplicationRegistrationBuilder();

// add app-specific attributes here
registrationBuilder.addAttribute("Attribute", "value");

ApplicationRegistration applicationRegistration = registrationBuilder.buildRegistration();

```