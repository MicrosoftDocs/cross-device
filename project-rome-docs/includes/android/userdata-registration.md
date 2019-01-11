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

### Step 7. Use UserData APIs with account​

Create UserDataFeed using account​
Register with AFS Service

```ObjectiveC
struct IUserDataFeed : IBase<UUID<0x46734a87, 0x602b, 0x4e4c, 0x88, 0xb5, 0x31, 0x3a, 0xa4, 0x3, 0x30, 0x98>>​
{​
static InterfacePtr<IUserDataFeed> GetForAccount(​
const InterfacePtr<IConnectedDevicesAccount>& account,​
const InterfacePtr<IConnectedDevicesPlatform>& platform, ​
const std::u16string& activitySourceHost);​
​
virtual void SubscribeToSyncScopesAsync(​
const std::vector<InterfacePtr<IUserDataFeedSyncScope>>& syncScopes, ​
AsyncCallback<bool>&& callback) = 0;​
…​
};​


Create UserDataFeed​
If Platform has not been started, it throws InvalidState exception with message of “Platform has not been started” ​
If Account has not been added into platform, it throws InvalidState exception with message of “Account needs to added into platform”​
If Account has not been registered for its notificationRegistration, it throws InvalidState Expetion with message of “Account has not registered its notificationRegistration”​
​
Call SubscribeToSyncScopesAsync to Save the notification registration registered in step 5 together with synscopes to AFS Services​
Check the async callback result​
If successful, App can start to use the rest UserData APIs​
If failed, App needs to retry SaveAsync at some point to make sure it is successfully completed in order to guarantee the rest of UserData APIs can be successfully used.

Notification Registration and its Renew with Services

In step 5.  we discussed above how app to inform platform how to receive service response notifications, either by push notification or polling (NotificationRegistratonManager.RegisterForAccountAsync)​
In step 6/7, we talked about how app to save that notification registration info to DDS/AFS Service separately​
IRemoteSystemAppRegistration::SaveAsync​
IUserDataFeed::SubscribeToSyncScopesAsync​
​
The notification registration can be out-of-date​
App receive new Push notification Token​
The notification Registration expired (App receive notification registration expiring/expired event from NotificationRegistrationManager)​
​
Either case, App needs to go through step 5 to get new notification registration for the account in use, and then call RemoteSystemApplication::SaveAsync or IUserDataFeed::SubscribeToSyncScopesAsync and make sure they succeeded in order to update notification registration on DDS/AFS services. 