---
title: include file
description: include file
ms.date: 07/17/2018
ms.assetid: 93f45482-14e4-4aec-8185-ee05b592215f
ms.localizationpriority: medium
---

If you wish to implement the **[MCDConnectedDevicesAccountManager](../../../includes/ios/auth-scopesiOS.md)** interface yourself, take note of the following information. If you're using an MSA, you will need to include the following scopes in your sign-in request: `"wl.offline_access"`, `"ccs.ReadWrite"`, `"dds.read"`, `"dds.register"`, `"wns.connect"`, `"asimovrome.telemetry"`, and `"https://activity.windows.com/UserActivity.ReadWrite.CreatedByApp"`. If you're using an AAD account, you'll need to request the following audiences: `"https://cdpcs.access.microsoft.com"`, `"https://cs.dds.microsoft.com"`, `"https://wns.windows.com/"`, and `"https://activity.microsoft.com"`.

Additionally, whether you use the provided **MCDConnectedDevicesAccountManager** implementation or not, if you are using AAD you'll need to specify the following permissions in your app's registration on the Azure portal (portal.azure.com > Azure Active Directory > App registrations): 
* Microsoft Activity Feed Service 
  * Deliver and modify user notifications for this app
  * Read and write app activity to users' activity feed
* Windows Notification Service
  * Connect your device to Windows Notification Service 
* Microsoft Device Directory Service
  * See your list of devices
  * Be added to your list of devices and apps 
* Microsoft Command Service
  * Communicate with user devices
  * Read user devices
