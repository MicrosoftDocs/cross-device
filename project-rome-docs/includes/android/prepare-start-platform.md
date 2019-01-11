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

Before starting the platform you'll need to subscribe to AccoutManager and NotificationRegistrationManager events​.

AccountManager

`struct IConnectedDevicesAccountManager : public IBase<UUID<0xD940F180, 0x0C11, 0x4C24, 0x99, 0x70, 0xC5, 0xCE, 0xCD, 0xC9, 0x61, 0xFC>>​
{​
virtual void AddAccountAsync(​
const InterfacePtr<IConnectedDevicesAccount>& account,​
AsyncCallback<InterfacePtr< >>&& callback) = 0;​
​
virtual void RemoveAccountAsync(​
const InterfacePtr<IConnectedDevicesAccount>& account,​
AsyncCallback<InterfacePtr<IConnectedDevicesRemoveAccountResult>>&& callback) = 0;​
​
virtual std::vector<InterfacePtr<IConnectedDevicesAccount>> GetAllAccounts() const = 0;​
​
virtual Event<const InterfacePtr<IConnectedDevicesAccountManager>&,​
const InterfacePtr<IConnectedDevicesAccessTokenRequestedEventArgs>&>&​
AccessTokenRequested() = 0;​
​
virtual Event<const InterfacePtr<IConnectedDevicesAccountManager>&,​
const InterfacePtr<IConnectedDevicesAccessTokenInvalidatedEventArgs>&>&​
AccessTokenInvalidated() = 0;​
};
`

NotificationManager

`
struct IConnectedDevicesNotificationRegistrationManager : IBase<UUID<0xefffb4d, 0xd36d, 0x440a, 0x9b, 0x64, 0xf8, 0xb8, 0xc9, 0x39, 0x35, 0x7d>>​
{​
virtual void RegisterForAccountAsync(​
const InterfacePtr<IConnectedDevicesAccount>& account,​
const InterfacePtr<IConnectedDevicesNotificationRegistration>& notificationRegistration, ​
AsyncCallback<bool>&& callback) = 0;​
​
virtual ConnectedDevicesNotificationRegistrationState GetNotificationRegistrationStateForAccount(​
const InterfacePtr<IConnectedDevicesAccount>& account) = 0; ​
​
virtual Event<const InterfacePtr<IConnectedDevicesNotificationRegistrationManager>&,​
const InterfacePtr<IConnectedDevicesNotificationRegistrationStateChangedEventArgs>&>&​
NotificationRegistrationStateChanged() = 0;​
};​
​
enum class ConnectedDevicesNotificationRegistrationState​
{​
Unregistered = 0,​
Registered,​
Expiring,​
Expired,​
};
`