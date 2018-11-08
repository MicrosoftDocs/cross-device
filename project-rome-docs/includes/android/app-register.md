---
title: include file
description: include file
ms.author: pafarley
author: PatrickFarley
ms.date: 07/17/2018
ms.topic: include
ms.assetid: 7ffe1891-788a-456d-9076-338485390204
ms.localizationpriority: medium
---

## Register app with the cloud directory

App registration is done through the **IRemoteSystemApplicationRegistration** interface. You may wish to put the following method in a separate helper class.

```Java

public static void registerApp(Context context, ArrayList<AppServiceProvider> appServiceProviders, LaunchUriProvider launchUriProvider, EventListener<UserAccount, CloudRegistrationStatus> listener) {
    
    // initialize the ApplicationRegistration with all possible services

    RemoteSystemApplicationRegistrationBuilder builder = new RemoteSystemApplicationRegistrationBuilder();
    // add app-specific attributes 
    builder.addAttribute("SampleAttribute", "Value");

    // Add the passed-in AppService and LaunchUri Providers to the registration builder
    if (appServiceProviders != null) {
        for (AppServiceProvider provider : appServiceProviders) {
            builder.addAppServiceProvider(provider);
        }
    }
    if (launchUriProvider != null) {
        builder.setLaunchUriProvider(launchUriProvider);
    }

    // Build the ApplicationRegistration instance
    IRemoteSystemApplicationRegistration registration = builder.buildRegistration();

    // Add the passed-in EventListener to handle registration completion
    registration.addCloudRegistrationStatusChangedListener(listener);
    // start cloud registration
    registration.start();
}
```

In your main class, after **Platform** initialization, add the following code to register the application. Note that app service providers (**[AppServiceProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.hosting._app_service_provider)**) and the URI launcher (**[LaunchUriProvider](https://docs.microsoft.com/java/api/com.microsoft.connecteddevices.hosting._launch_uri_provider)**), which are only needed for certain scenarios, are not provided at this step.

```Java
RegistrationHelperClass.register(this, null, null, new EventListener<UserAccount, CloudRegistrationStatus>() {
    // define an event listener to handle the cloud registration operation:
    @Override
    public void onEvent(UserAccount account, CloudRegistrationStatus status) {
        switch (status) {
            case NOT_STARTED:
                Log.d(TAG, "Registration has not started.");
                break;
            case IN_PROGRESS:
                Log.d(TAG, "Registration in progress...");
                break;
            case SUCCEEDED:
                Log.d(TAG, "Completed Rome registration");
                // do other work now that registration has succeeded
                break;
            case FAILED:
                Log.d(TAG, "Rome registration failed!");
                break;
        }
    }
});
```
