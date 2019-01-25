---
title: include file
description: include file
ms.date: 07/17/2018
ms.assetid: 93f45482-14e4-4aec-8185-ee05b592215f
ms.localizationpriority: medium
---

### Set up authentication and account management

The Connected Devices Platform requires a valid OAuth token to be used in the registration process.  You may use your preferred method of generating and managing the OAuth tokens.  However, to help developers get started using the platform, we've included an authentication provider as a part of the [iOS sample app](https://github.com/Microsoft/project-rome/tree/master/iOS/samples/account-provider-sample) that generates and manages refresh tokens for your convenience.

If you do not use the provided code, you will need to implement the **[MCDConnectedDevicesAccountManager](../objectivec-api/connecteddevices/MCDConnectedDevicesAccountManager.md)** interface yourself. If you're using an MSA, include the following scopes in your sign-in request: `"wl.offline_access"`, `"ccs.ReadWrite"`, `"dds.read"`, `"dds.register"`, `"wns.connect"`, `"asimovrome.telemetry"`, and `"https://activity.windows.com/UserActivity.ReadWrite.CreatedByApp"`. If you're using an AAD account, you'll need to request the following audiences: `"https://cdpcs.access.microsoft.com"`, `"https://cs.dds.microsoft.com"`, `"https://wns.windows.com/"`, and `"https://activity.microsoft.com"`.

Whether you use the provided **MCDConnectedDevicesAccountManager** implementation or not, if you are using AAD you'll need to specify the following permissions in your app's registration on the Azure portal (portal.azure.com > Azure Active Directory > App registrations): 
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
