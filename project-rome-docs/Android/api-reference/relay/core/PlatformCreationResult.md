---
title: PlatformCreationResult
description:  This class is the result of an attempt to initialize a Platform.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# PlatformCreationResult class

```
public final class PlatformCreationResult
```  

This class is the result of an attempt to initialize a Platform.

## Methods

### getStatus
`public PlatformCreationStatus getStatus()`

Gets the status of the Platform initialization attempt.

#### Returns 
A [PlatformCreationStatus](PlatformCreationStatus.md) value describing the status.

### getPlatform
`public Platform getPlatform()`

Gets the initialized Platform if the attempt was successful.

#### Returns 
The initialized [Platform](Platform.md) instance if available, otherwise `null`.

## Example

The following sample code sets up the initialization of a Platform instance. 

```Java
ApplicationRegistrationBuilder registrationBuilder = new ApplicationRegistrationBuilder();

// add app-specific attributes here
registrationBuilder.addAttribute("Attribute", "value");

ApplicationRegistration applicationRegistration = registrationBuilder.buildRegistration();

// Instantiate Platform using the UserAccountProvider the sign-in helper provides
// NotificationProvider is used for hosting capabilities (optional), so we pass in null
AsyncOperation<PlatformCreationResult> resultOperation = Platform.createInstanceAsync(
        this, null, applicationRegistration, getSignInHelper());

// Can handle success/failure to create platform, simply give a toast
resultOperation.whenCompleteAsync(new AsyncOperation.ResultBiConsumer<PlatformCreationResult, Throwable>()
{
        @Override
        public void accept(PlatformCreationResult platformCreationResult, Throwable throwable) throws Throwable
        {
        Log.d("accept", "Entered accept");
        if (throwable != null)
                return;

        if (platformCreationResult.getStatus() == PlatformCreationStatus.FAILURE)
                return;

        // save instance of successfully created Platform
        mPlatform = platformCreationResult.getPlatform();
        mPlatformInitialized = true;

        }
});
```