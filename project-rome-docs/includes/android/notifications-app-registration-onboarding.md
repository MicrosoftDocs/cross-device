---
title: include file
description: include file
ms.topic: include
ms.assetid: bbef84bf-a6b7-44be-879d-0fa6065e37b1
ms.localizationpriority: medium
---

### MSA and AAD Authentication Registration

Microsoft Account (MSA) or Azure Active Directory (AAD) authentication registration is required for all features of the SDK including Notifications, except for the Nearby sharing APIs. 

If you do not already have an MSA and wish to use one, register on [account.microsoft.com](https://account.microsoft.com/account).

Next, if you are using MSA as the authentication and identity framework for your users, you must register your app with Microsoft by following the instructions on the [Application Registration Portal](https://apps.dev.microsoft.com/) (if you do not have a Microsoft developer account, you must create one first). You should receive a client ID string for your app; make sure to remember the location or save this. Later this will be used during Graph Notifications onboarding. 
Note that an app using MSA authentication needs to be registered as a Live SDK application as shown below.
![Application Registration Portal](../../msgraph-notifications/media/msa_app_registration/app_registration_portal.png)

If you're writing an app that uses AAD as work account or school account authentication and identity framework, you must register your app via [Azure Active Directory Authentication Libraries](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-libraries) in order to get the client ID, as shown below. 
 ![AAD Registration Portal](../../msgraph-notifications/media/aad_registration_portal/aad_registration_portal.png)
When creating a new app registration, there are a few permissions required in order to use Graph Notifications and other connected device platform capabilities. Please see below. 
![AAD Registration Portal – Setting – Required Permissions](../../msgraph-notifications/media/aad_registration_portal/aad_registration_portal_permissions.png)
* Add user sign-in permission shown as below.
![Required Permissions – AAD User Profile](../../msgraph-notifications/media/aad_registration_portal/permissions_1_user.png)
* Add Command Service permissions for device information, shown as below.
![Required Permissions – Devices](../../msgraph-notifications/media/aad_registration_portal/permissions_2_devices.png)
* Add Graph Notifications permission under Activity Feed Service APIs, shown as below.
![Required Permissions – Devices](../../msgraph-notifications/media/aad_registration_portal/permissions_3_graph_notifications.png)
* At the end, if you are writing cross-platform application including an UWP app running on Windows, make sure to add Windows Notification Service permission, shown as below. 
![Required Permissions – WNS](../../msgraph-notifications/media/aad_registration_portal/permissions_4_wns_push.png)
