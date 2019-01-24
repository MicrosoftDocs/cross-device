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

### Setup the platform

To get started simply instantiate the platform.

`ConnectedDevicesPlatform sPlatform = new ConnectedDevicesPlatform(context);`

### Subscribe to ConnectedDevicesAccountManager events to handle the user account 

The platform requires an authenicated user to access the platform.  You'll need to subscribe to **ConnectedDevicesAccountManager** events to ensure a valid account is being used. 

```Java
 ConnectedDevicesPlatform sPlatform.getAccountManager().accessTokenRequested().subscribe((accountManager, args) -> {

    // Get access token
                 
}
```

```Java
 ConnectedDevicesPlatform sPlatform.getAccountManager().accessTokenInvalidated().subscribe((accountManager, args) -> {

    // Refresh and renew existing access token
}
```


### Subscribe to ConnectedDevicesNotificationRegistrationManager events

Similarly, the platform uses notifications to deliver commands between devices.  Therefore, you must subscribe to the **ConnectedDevicesNotificationRegistrationManager** events to ensure the cloud registration states are valid for the account being used.  Verify the the state using **ConnectedDevicesNotificationRegistrationState**

```Java
ConnectedDevicesPlatform sPlatform.getNotificationRegistrationManager().notificationRegistrationStateChanged().subscribe((notificationRegistrationManager, args) -> {
    
     // Check state using **ConnectedDevicesNotificationRegistrationState** enum

}
```
### Start the platform
Now that the platform is initialized and event handlers are in place, you are ready to start discovering remote system devices.  

`ConnectedDevicesPlatform sPlatform.start();`

### Retrieve user accounts known to the app

It is important to ensure that the list of user accounts known to the app are properly synchronized with the **ConnectedDevicesAccountManager**.

Use **ConnectedDevicesAccountManager.addAccountAsync** to add a new user account.

```Java
 public synchronized AsyncOperation<ConnectedDevicesAddAccountResult> addAccountToAccountManagerAsync(ConnectedDevicesAccount account) {
        return ConnectedDevicesPlatform sPlatform.getAccountManager().addAccountAsync(account);
    }
```

To remove an invalid account you can use **MCDConnectedDevicesAccountManager.removeAccountAsync**

```Java
 public synchronized AsyncOperation<ConnectedDevicesAddAccountResult> removeAccountToAccountManagerAsync(ConnectedDevicesAccount account) {
        return ConnectedDevicesPlatform sPlatform.getAccountManager().removeAccountAsync(account);
    }
```