---
title: include file
description: include file
ms.author: pafarley
author: PatrickFarley
ms.date: 07/17/2018
ms.topic: include
ms.prod: windows
ms.technology: connected-devices
ms.assetid: 7282aec9-0e80-49bd-ace0-636d9fd16acb
ms.localizationpriority: medium
---

## Register app with the cloud directory

App registration is done through the **MCDRemoteSystemApplicationRegistration** class. Create an instance by using the **MCDRemoteSystemApplicationRegistrationBuilder** class, optionally adding in app service providers (**[MCDAppServiceProvider](../../objectivec-api/hosting/MCDAppServiceProvider.md)**) and a URI launcher (**[MCDLaunchUriProvider](../../objectivec-api/hosting/MCDLaunchUriProvider.md)**); these are only needed for certain scenarios and are not required at this step.

The following code from the sample app shows the registration of the app. Registration code should go directly below the platform initialization code. 

```ObjectiveC
- (void)initializePlatform
{
    // ...

    // App is registered asynchronously.
    MCDHostingRemoteSystemApplicationRegistrationBuilder* builder = [MCDHostingRemoteSystemApplicationRegistrationBuilder new];
    [builder setLaunchUriProvider:[[LaunchUriProvider alloc] initWithDelegate:[AppDataSource sharedInstance].inboundRequestLogger]];
    [builder addAppServiceProvider:[[AppServiceProvider alloc] initWithDelegate:[AppDataSource sharedInstance].inboundRequestLogger]];
    [builder addAttribute:@"ExampleAttribute" forName:@"ExampleName"];
    MCDRemoteSystemApplicationRegistration* registration = [builder buildRegistration];
    
    [registration addCloudRegistrationStatusChangedListener:^(MCDUserAccount * _Nonnull account, MCDCloudRegistrationStatus status) {
        NSLog(@"Cloud Registration Status Changed listener");
        switch (status) {
            case MCDCloudRegistrationStatusFailed:
                NSLog(@"Cloud registration completed with status Failed");
                break;
            case MCDCloudRegistrationStatusInProgress:
                NSLog(@"Cloud registration in progress");
                break;
            case MCDCloudRegistrationStatusNotStarted:
                NSLog(@"Cloud registration not started");
                break;
            case MCDCloudRegistrationStatusSucceeded:
                dispatch_async(dispatch_get_main_queue(), ^{
                    // The app has been registered.  It is safe to enable button.
                    [self.deviceRelayButton setEnabled:YES];
                    [self.activityFeedButton setEnabled:YES];
                });
                break;
        }
    }];
    
    [registration start];
}
```