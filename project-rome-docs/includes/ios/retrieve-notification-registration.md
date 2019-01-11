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

### Prepare account that will be used by the platform

Need retrieve notificationRegistration info from WNS service​

provide a way to receive/retrieve Rome Service reqeuest response

App needs to tell platform either using push notification/Polling for that​
App invoke NotificationRegistratonManager::RegisterForAccountAsync with NotificationRegistration, on which App can specify NotificatonType to receive the response. ​
enum class ConnectedDevicesNotificationType​
{​
Unknown = 0,​
WNS,​
GCM,​
FCM,​
APN,​
Polling,​
};​

App should always check async callback to see if registration is successful or not. ​
If failed,  App needs to retry at some point to register the notificaciontRegistration for this account again in order to for this account to be usable by RemoteSystem/UserData APIs.  ​
If successful, this account is ready to be used by RemoteSystem/UserData APIs