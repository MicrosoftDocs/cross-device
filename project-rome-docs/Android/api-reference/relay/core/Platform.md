---
title: Platform
description:  A static class to perform global scale commands to the Connected Devices Platform.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# Platform class

```
public final class Platform
```  

A static class to perform global scale commands to the Connected Devices Platform.

## Methods

### shutdownAsync
`public AsyncOperation<Void> shutdownAsync()`

Shuts down the Remote Systems Platform.

### createInstanceAsync
`public static AsyncOperation<PlatformCreationResult> createInstanceAsync(@NonNull Context context,
        @Nullable NotificationProvider notificationProvider, @NonNull IApplicationRegistration applicationRegistration,
        @NonNull UserAccountProvider accountProvider)`

Initializes the Connected Devices Platform. This must be invoked before attempting to use any Connected Devices functionality.

#### Parameters
* `context` The context of the calling application. This is needed to expose app-specific resources to the Connected Devices Platform.
* `notificationProvider` The ID of the notification provider for this platform instance.
* `applicationRegistration` The ID of the application registration for this platform instance.
* `accountProvider` The ID of the user account provider for this platform instance.

#### Returns
* An asynchronous operation with a [PlatformCreationResult](PlatformCreationResult.md), which contains an Platform instance.

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