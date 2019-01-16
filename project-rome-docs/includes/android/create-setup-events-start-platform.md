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

## Create the platform

To get started simply instantiate the platform and hook the event handlers before calling <TODO>ConnectedDevicesPlatform.Start(). After <TODO>Start() is called events may begin to fire.

m_platform = new ConnectedDevicesPlatform(); - INITIALIZE PLATFORM

## Setup event handlers for AccountManager and NotificationRegistartionManager

The platform requires an authenicated user to access the platform.  The  class is used to <TODO>.  We need to make sure the event handlers are in place for the AccountManager before using the platform.   Likewise, the platform uses notifications to deliver commands between devices.  The NotficationRegistrationManager class is used to mange all notifications.  The NotificationManger events NotificationManagerChanged must be setup during this step as well.

m_platform.AccountManager.AccessTokenRequested += AccountManager_AccessTokenRequestedAsync; - SETUP EVENT HANDLERS FOR ACCOUNTMANAGER
m_platform.AccountManager.AccessTokenInvalidated += AccountManager_AccessTokenInvalidated;
m_platform.NotificationRegistrationManager.NotificationRegistrationStateChanged += NotificationRegistrationManager_NotificationRegistrationStateChanged; - SETUP EVENT HANDLERS FOR MOTIFICATIONMANAGER

## Start the platform
We are ready to start discovering remote system devices by calling start() on the MCDConnectedDevicesPlatform class.

m_platform.Start(); - START THE PLATFORM

# Retrieve accounts

It is important to ensure that the list of accounts known to the app are properly synchronized with the MCDConnectedDevicesPlatform.AccountManager.

Accounts can be in 3 different scenarios:
    1: cached account in good standing (initialized in the SDK and our token cache).
    2: account missing from the SDK but present in our cache: Add and initialize account.
    3: account missing from our cache but present in the SDK. Log the account out async

    Project Rome features (e.g. subcomponents), such as Device Relay, can only be initialized when an account is in both the app cache and the SDK cache.
    For scenario 1, immediately initialize our subcomponents.
    For scenario 2, subcomponents will be initialized after <TODO>InitializeAccountAsync registers the account with the SDK.
    For scenario 3, InitializeAccountAsync will unregister the account and subcomponents will never be initialized.

<TODO>
    // Add all our cached accounts.
            var sdkCachedAccounts = m_platform.AccountManager.Accounts.ToList();
            var appCachedAccounts = ApplicationData.Current.LocalSettings.Values[AccountsKey] as string;
            if (!String.IsNullOrEmpty(appCachedAccounts))
            {
                DeserializeAppCachedAccounts(appCachedAccounts, sdkCachedAccounts);
            }

            // Add the remaining SDK only accounts (these need to be removed from the SDK)
            foreach (var sdkCachedAccount in sdkCachedAccounts)
            {
                m_accounts.Add(new Account(m_platform, sdkCachedAccount.Id, sdkCachedAccount.Type, null, AccountRegistrationState.InSdkCacheOnly));
            }

# Initialize the account list

Finally initialize the accounts. This will refresh registrations when needed, add missing accounts, and remove stale accounts from the <TODO>ConnectedDevicesPlatform.AccountManager.

            // All accounts which can be in a good state should be. Remove any accounts which aren't
            m_accounts.RemoveAll((x) => x.RegistrationState != AccountRegistrationState.InAppCacheAndSdkCache);
            AccountListChanged();

The following code from the sample app shows the how to get started using the platform. 

```Java

```