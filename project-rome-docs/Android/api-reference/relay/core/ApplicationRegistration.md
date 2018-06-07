---
title: ApplicationRegistration
description: This class represents an application that is registered for remote connectivity.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# ApplicationRegistration class

```
public final class ApplicationRegistration implements IApplicationRegistration
```

This class represents an application that is registered for remote connectivity. It can provide remote app services or be used to launch a URI.

## Methods

### getAttributes 
`public Map<String, String> getAttributes()`

Gets the attributes associated with this application. For example, your app could define a unique ID attribute and share it with client devices. Then they can look for it in subsequent discoveries.

#### Returns
A Map of key/value pairs defining the attributes of this registration.

## Example

The following sample code uses an ApplicationRegistrationBuilder to create an ApplicationRegistration instance. 

```Java
ApplicationRegistrationBuilder registrationBuilder = new ApplicationRegistrationBuilder();

// add app-specific attributes here
registrationBuilder.addAttribute("Attribute", "value");

ApplicationRegistration applicationRegistration = registrationBuilder.buildRegistration();

```
