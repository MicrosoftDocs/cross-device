---
title: include file
description: include file
ms.author: lahugh
author: laurenhughes
ms.date: 09/21/2018
ms.topic: include
ms.assetid: 0397d8a8-3526-4ef8-9c83-3ade2ba0f951
ms.localizationpriority: medium
---

# How-To Guide: Integrating with Graph Notifications (Android)

With the Project Rome client-side SDK on Android, your Android app can perform the necessary registration steps to become a receiving endpoint that receives notifications published from your app server targeted at a user. The SDK is then used to manage the notifications on the client side including accessing new notification payloads received by this client, manage the state of notifications, and retrieving notification history. For more information about Notifications and how it enables human-centric notification delivery, see [Microsoft Graph Notifications Overview](../../index.md)

See the [API reference](../android/api-reference/index.md) page for links to the reference docs relevant to notification scenarios.

## Preliminary setup for accessing the Connected Devices Platform in order to use Graph Notifications 
There are a few steps you must take to integrate with Graph Notifications
* MSA or AAD App Registration
* Dev Center Onboarding to Provide Cross-Platform App Identity and Push Notification Credentials
* Adding the SDK and Initializing the Connected Devices Platform
* Associate the Notification Service with Connected Devices Platform

First, you must complete the MSA and/or AAD App Registration. If you've done this already, skip to the next section.
[!INCLUDE [android/platform-init](../../../includes/android/notifications-app-registration-onboarding.md)]
Next, you must onboard with Microsoft Windows Dev Center to get access to the Connected Device Platform in order to integrate with cross-device experiences including use of Graph Notifications. If you've done this already, skip to the next section.
[!INCLUDE [android/notification-init](../../../includes/android/notifications-dev-center-onboarding.md)]
Next, you must add the Project Rome SDK to your project and initialize the Connected Devices Platform. If you've done this already, skip to the next section.
[!INCLUDE [android/notification-init](../../../includes/android/notifications-platfrom-init.md)]
Lastly, you must enable your app to receive push notifications. If you've done this already, skip to the next section.
[!INCLUDE [android/notification-init](../../../includes/android/notifications-notification-init.md)]

## Initialize a Graph Notification channel
At a high level, the SDK allows your app to subscribe to different channels in order to receive and manage different types of User Data – including Graph Notifications, User Activities, and more. These are all stored and synced in **UserDataFeed**. **UserNotification** is the class and data type corresponding to a user-targeted notification sent via Graph Notifications. 
To integrate with Graph Notification and start receiving UserNotification published by your app server, you will first need to initialize the user data feed by creating a **UserNotificationChannel**. You should treat this like the platform initialization step above: it should be checked and possibly redone whenever the app comes to the foreground (but not before platform initialization). 

The following methods initialize a **UserNotificationChannel**.

```Java
private UserNotificationChannel mNotificationChannel;
private UserDataFeed mUserDataFeed;

// ...

/**
 * Initializes the UserNotificationFeed.
 */
public void initializeUserNotificationFeed() {

    // define what scope of data this app needs
    SyncScope[] scopes = { UserNotificationChannel.getSyncScope() };

    // Get a reference to the UserDataFeed. This method is defined below
    mUserDataFeed = getUserDataFeed(scopes, new EventListener<UserDataFeed, Void>() {
        @Override
        public void onEvent(UserDataFeed userDataFeed, Void aVoid) {
            if (userDataFeed.getSyncStatus() == UserDataSyncStatus.SYNCHRONIZED) {
                // log synchronized.
            } else {
                // log synchronization not completed.
            }
        }
    });

    // this method is defined below
    mNotificationChannel = getUserNotificationChannel();
}

// instantiate the UserDataFeed
private UserDataFeed getUserDataFeed(SyncScope[] scopes, EventListener<UserDataFeed, Void> listener) {
    UserAccount[] accounts = AccountProviderBroker.getSignInHelper().getUserAccounts();
    if (accounts.length <= 0) {
        // notify the user that sign-in is required
        return null;
    }

    // use the initialized Platform instance, along with the cross-device app ID.
    UserDataFeed feed = UserDataFeed.getForAccount(accounts[0], PlatformBroker.getPlatform(), Secrets.APP_HOST_NAME);
    feed.addSyncStatusChangedListener(listener);
    feed.addSyncScopes(scopes);
    // sync data with the server
    feed.startSync();
    return feed;
}

// use the UserDataFeed reference to create a UserActivityChannel
@Nullable
private UserNotificationChannel getUserNotificationChannel() {
    UserNotificationChannel channel = null;
    try {
        // create a UserNotificationChannel for the signed in account
        channel = new UserNotificationChannel(mUserDataFeed);
    } catch (Exception e) {
        e.printStackTrace();
        // handle exception
    }
    return channel;
}
```
At this point, you should have a **UserNotificationChannel** reference in `mNotificationChannel`.

## Create a UserNotificationReader to receive incoming UserNotifications and access UserNotification history
As we showed previously, the initial Google Cloud Messaging notification arriving on the app client only contains a shoulder tap, and you need to pass that shoulder tap payload to the Connected Devices Platform in order to trigger the SDK to perform a full sync with the Connected Device server, which contains all the UserNotifications published by your app server. This will pull down the full notification payload published by your app server corresponding to this shoulder tap (and in case if any previous notifications were published but not received on this app client due to device connectivity or other issues, they will be pulled down as well). With these real-time syncs constantly performed by the SDK, the app client is able to have access to a local cache of this logged-in user’s UserNotification data feed. 
A UserNotificationReader in this case enables the app client’s access to this data feed – to receive latest notification payload via event listener, or to access the full UserNotification collection which can be used as view model of the user’s notification history.  
### Receiving UserNotifications
First you need to instantiate a UserNotificationReader, and get all the existing UserNotifications already in the reader if you are interested in consuming that information for the experience you are trying to enable. It’s safe to always assume that the app server has already published notifications to this logged in user, given that this particular device endpoint might not be the only or the first endpoint that the user has installed your app. 
```Java
private static UserNotificationReader mReader;
private static final ArrayList<UserNotification> mHistoricalNotifications = new ArrayList<>();
// Instantiate UserNotificationReader
UserNotificationReaderOptions options = new UserNotificationReaderOptions();
mReader = mNotificationChannel.createReaderWithOptions(options);
// Read any previously published UserNotifications that have not expired yet
mReader.readBatchAsync(Long.MAX_VALUE).thenAccept(new AsyncOperation.ResultConsumer<UserNotification[]>() {
    @Override
    public void accept(UserNotification[] userNotifications) throws Throwable {
        synchronized (mHistoricalNotifications) {
            for (UserNotification notification : userNotifications) {
                if (notification.getReadState() == UserNotificationReadState.UNREAD) {
                    mHistoricalNotifications.add(notification);
                }
            }
        }
 
        if (RunnableManager.getHistoryUpdated() != null) {
            activity.runOnUiThread(RunnableManager.getHistoryUpdated());
        }
    }
});

```
Now, add an event listener which gets triggered when the Connected Device Platform completes a sync and has new changes to notify you about. In the case of Graph Notifications, new changes could be new incoming UserNotifications published by your app server, or UserNotifcation updates, deletions, and expirations that happened from the server or from other registered endpoints that the same user logged in. 
> [!TIP] 
> This event listener is where you handle the main business logic and “consume” the content of your notification payload based on your scenarios. If you currently use Google Cloud Messaging’s data message to construct a visual notification in the OS-level notification tray, or if you use the content in the notification to update some in-app UI, this is the place to do that. 
```Java
mReader.addDataChangedListener(new EventListener<UserNotificationReader, Void>() {
    @Override
    public void onEvent(UserNotificationReader userNotificationReader, Void aVoid) {
        userNotificationReader.readBatchAsync(Long.MAX_VALUE).thenAccept(new AsyncOperation.ResultConsumer<UserNotification[]>() {
        @Override
        public void accept(UserNotification[] userNotifications) throws Throwable {
            boolean updatedNew = false;
            boolean updatedHistorical = false;
            synchronized (sHistoricalNotifications) {
                for (final UserNotification notification : userNotifications) {
                    if (notification.getStatus() == UserNotificationStatus.ACTIVE && notification.getReadState() == UserNotificationReadState.UNREAD) {
                        switch (notification.getUserActionState()) {
                            case NO_INTERACTION:
                                // Brand new notification
                                // Insert business logic to construct a new visual notification in Android notification tray for the user to see
                                // ...
                            case DISMISSED:
                                // Existing notification that is marked as dismissed
                                // An app client receive this type of changes because another app client logged in by the same user has marked the notification as dismissed and the change is fanned-out to everywhere
                                // This state sync across app clients on different devices enable universal dismiss of notifications and other scenarios across multiple devices owned by the same user
                                // Insert business logic to dismiss the corresponding visual notification inside Android system notification tray, to make sure users don’t have to deal with redundant information across devices, and potentially insert this notification in your app’s notification history view
                                // ...
                            default:
                                // Unexpected
                        }
                    } else {
                        // ...
                    }
                }
            }
        }
    });
}
});

```
## Update the state of an existing UserNotification
In the previous section, we mentioned that sometimes a UserNotification change received through the reader could be a state update on an existing UserNotification – whether that’s being marked as dismissed or marked as read. In this case, the app client can choose what to do, such as enabling universal dismiss by removing the corresponding visual notification on this particular device. 
Taking a step back, your app client is often the one that initiated this UserNotification change update to begin with – from a different device. You can choose the time to update the state of your UserNotifications, but usually they get updated when the corresponding visual notification is handled by the user on that device, or the notification is further handled by the user in some in-app experience you enable. 
Here is an example of what the flow would look like:
Your app server publishes a notification targeted at User A. User A receives this notification on both his PC and his phone where the app clients are installed. The user clicks on the notification on PC, and chases into the app to handles the corresponding task. The app client on this PC will then call into Connected Devices Platform SDK to update the state of the corresponding UserNotification in order to have this update synced across all this user’s devices. The other app clients, upon receiving this state update in real-time, will then remove the corresponding visual alert / message / toast notification from the device’s notification center / notification tray / Action Center. This is how notifications get universally dismissed across a user’s devices. 

> [!TIP] 
> UserNotification class currently provides 2 types of state updates – you can modify the UserNotificationReadState or the UserNotificationUserActionState and define your own logic on what should happen when notifications are updated. For example, you can mark UserActionState to be Activated or Dismissed, and pivot on that value to implement universal dismiss. Alternatively, or at the same time you can mark ReadState as Read or Unread and based on that determine which notifications should show up in the in-app notification history view. 
Below code snippet shows how to mark the UserNotificationUserActionState of a notification as Dismissed.

```Java
public void dismissNotification(int position) {
    final UserNotification notification = mNewNotifications.get(position);
          
    notification.setUserActionState(UserNotificationUserActionState.DISMISSED);
    notification.saveAsync();
}

```
