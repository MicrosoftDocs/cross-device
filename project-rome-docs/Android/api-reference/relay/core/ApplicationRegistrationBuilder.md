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