---
title: include file
description: include file
ms.author: carmenf
author: CarmenForsmann
ms.date: 01/10/2019
ms.topic: include
ms.assetid: 
ms.localizationpriority: medium
---

### Begin RemoteSystem registration
Account is ready to be used!  

`
struct IRemoteSystemAppRegistration : IBase<UUID<0xA0274713, 0x7FB6, 0x414F, 0xA9, 0x46, 0xCD, 0x47, 0x9F, 0xDE, 0x2D, 0x15>>​
{​
        static InterfacePtr<IRemoteSystemAppRegistration> GetForAccount(​
                const InterfacePtr<IConnectedDevicesAccount>& account,​
                const InterfacePtr<IConnectedDevicesPlatform>& platform);​
​
        virtual void SaveAsync(AsyncCallback<bool>&& callback) = 0;​
​
        virtual void SetAppServiceProviders(const std::vector<InterfacePtr<IAppServiceProvider>>& appServiceProviders) = 0;​
        virtual void SetLaunchUriProvider(const InterfacePtr<ILaunchUriProvider>& launchUriProvider) = 0;​
…​
};
`
​
Create RemoteSystemAppregistration​
If Platform has not been started, it throws InvalidState exception with message of “Platform has not been started” ​
If Account has not been added into platform, it throws InvalidState exception with message of “Account needs to added into platform”​
If Account has not been registered for its notificationRegistration, it throws InvalidState Expetion with message of “Account has not registered its notificationRegistration”

Call SetAppServiceProvider/SetLaunchUriProvider if App can provide one, after which, Platform is ready for processing incoming notifications for App Services/Launch Uri request.​
​
Call SaveAsync to Save the notification registration that gets registered in step 5 to DDS Service​
Check the async callback result​
If successful, App can start to use the rest RemoteSystemAPIs and expect response will be notified or retrieved successful. If using push notification, App can expect app service/launch URI incoming messages can be delivered. ​
If failed, App needs to retry SaveAsync at some point to make sure it is successfully completed in order to guarantee the rest of RemoteSystemAPIs can be successfully used.
