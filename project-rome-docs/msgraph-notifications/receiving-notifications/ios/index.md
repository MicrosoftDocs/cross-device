# How-To Guide: Integrating with Graph Notifications (iOS)

With the Project Rome client-side SDK on iOS, your iOS app can perform the necessary registration steps to become a receiving endpoint that receives notifications published from your app server targeted at a user. The SDK is then used to manage the notifications on the client side including accessing new notification payloads received by this client, manage the state of notifications, and retrieving notification history. For more information about Notifications and how it enables human-centric notification delivery, see [Microsoft Graph Notifications Overview](../../index.md)

See the [API reference](../api-reference/index.md) page for links to the reference docs relevant to notification scenarios.

## Preliminary setup for accessing the Connected Devices Platform in order to use Graph Notifications 
There are a few steps you must take to integrate with Graph Notifications
* MSA or AAD App Registration
* Dev Center Onboarding to Provide Cross-Platform App Identity and Push Notification Credentials
* Adding the SDK and Initializing the Connected Devices Platform
* Associate the Notification Service with Connected Devices Platform

First, you must complete the MSA and/or AAD App Registration. If you've done this already, skip to the next section.
[!INCLUDE [ios/notifications-app-registration-onboarding](../../../includes/ios/notifications-app-registration-onboarding.md)]
Next, you must onboard with Microsoft Windows Dev Center to get access to the Connected Device Platform in order to integrate with cross-device experiences including use of Graph Notifications. If you've done this already, skip to the next section.
[!INCLUDE [ios/notifications-dev-center-onboarding](../../../includes/ios/notifications-dev-center-onboarding.md)]
Next, you must add the Project Rome SDK to your project and initialize the Connected Devices Platform. If you've done this already, skip to the next section.
[!INCLUDE [ios/notifications-platform-init](../../../includes/ios/notifications-platfrom-init.md)]
Lastly, you must enable your app to receive push notifications. If you've done this already, skip to the next section.
[!INCLUDE [ios/notifications-notification-init](../../../includes/ios/notifications-notification-init.md)]

## Initialize a Graph Notification channel
At a high level, the SDK allows your app to subscribe to different channels in order to receive and manage different types of User Data – including Graph Notifications, User Activities, and more. These are all stored and synced in **MCDUserDataFeed**. **MCDUserNotification** is the class and data type corresponding to a user-targeted notification sent via Graph Notifications. 
To integrate with Graph Notification and start receiving MCDUserNotification published by your app server, you will first need to initialize the user data feed by creating a **MCDUserNotificationChannel**. You should treat this like the platform initialization step above: it should be checked and possibly redone whenever the app comes to the foreground (but not before platform initialization). 

The following methods initialize a **MCDUserNotificationChannel**.
```ObjectiveC
// You must be logged in to use UserNotifications
NSArray<MCDUserAccount*>* accounts = [[AppDataSource sharedInstance].accountProvider getUserAccounts];
if (accounts.count > 0)
{
    // Get a UserNotification channel, getting the default channel        
    NSLog(@"Creating UserNotificationChannel");
    NSArray<MCDUserAccount*>* accounts = [[AppDataSource sharedInstance].accountProvider getUserAccounts];
    MCDUserDataFeed* userDataFeed = [MCDUserDataFeed userDataFeedForAccount:accounts[0]
        platform:[AppDataSource sharedInstance].platform
        activitySourceHost:CROSS_PLATFORM_APP_ID];
    NSArray<MCDSyncScope*>* syncScopes = @[ [MCDUserNotificationChannel syncScope] ];
    [userDataFeed addSyncScopes:syncScopes];
    self.channel = [MCDUserNotificationChannel userNotificationChannelWithUserDataFeed:userDataFeed];
}
else
{
    NSLog(@"Must log in to receive notifications for the logged in user!");
    self.createNotificationStatusField.text = @"Need to be logged in!";
}
```
At this point, you should have a **MCDUserNotificationChannel** reference in `channel`.

## Create a MCDUserNotificationReader to receive incoming MCDUserNotifications and access MCDUserNotification history
As we showed previously, the initial APNS silent message arriving on the app client only contains a shoulder tap, and you need to pass that shoulder tap payload to the Connected Devices Platform in order to trigger the SDK to perform a full sync with the Connected Device server, which contains all the MCDUserNotifications published by your app server. This will pull down the full notification payload published by your app server corresponding to this shoulder tap (and in case if any previous notifications were published but not received on this app client due to device connectivity or other issues, they will be pulled down as well). With these real-time syncs constantly performed by the SDK, the app client is able to have access to a local cache of this logged-in user’s MCDUserNotification data feed. 
A MCDUserNotificationReader in this case enables the app client’s access to this data feed – to receive latest notification payload via event listener, or to access the full MCDUserNotification collection which can be used as view model of the user’s notification history.  
### Receiving MCDUserNotifications
First you need to instantiate a MCDUserNotificationReader, and get all the existing MCDUserNotifications already in the reader if you are interested in consuming that information for the experience you are trying to enable. It’s safe to always assume that the app server has already published notifications to this logged in user, given that this particular device endpoint might not be the only or the first endpoint that the user has installed your app. 
Then, add an event listener which gets triggered when the Connected Device Platform completes a sync and has new changes to notify you about. In the case of Graph Notifications, new changes could be new incoming MCDUserNotifications published by your app server, or MCDUserNotifcation updates, deletions, and expirations that happened from the server or from other registered endpoints that the same user logged in. 
> [!TIP] 
> This event listener is where you handle the main business logic and “consume” the content of your notification payload based on your scenarios. If you currently use APNS silent notification to construct a visual notification in the OS-level notification center, or if you use the content in the silent notification to update some in-app UI, this is the place to do that. 
```ObjectiveC
// Instantiate the reader from a MCDUserNotificationChannel
// Add a data change listener to subscribe to new changes when new notifications or notification updates are received
- (void)setupWithAccount:(MCDUserAccount*)account {
    dispatch_async(dispatch_get_global_queue(QOS_CLASS_DEFAULT, 0), ^{
        @synchronized (self) {
            MCDUserDataFeed* dataFeed = [MCDUserDataFeed userDataFeedForAccount:account platform:_platform activitySourceHost:@"graphnotifications.sample.windows.com"];
            [dataFeed addSyncScopes:@[[MCDUserNotificationChannel syncScope]]];
            self.channel = [MCDUserNotificationChannel userNotificationChannelWithUserDataFeed:dataFeed];
            self.reader = [self.channel createReader];
            
            __weak typeof(self) weakSelf = self;
            _readerRegistrationToken = [self.reader addDataChangedListener:^(__unused MCDUserNotificationReader* source) {
                NSLog(@"ME123 Got a change!");
                if (weakSelf) {
                    [weakSelf forceRead];
                } else {
                    NSLog(@"ME123 WEAKSELF FOR CHANGES IS NULL!!!");
                }
            }];
            
            [self forceRead];
        }
    });
}

// this is your own business logic when the event listener is fired
// In this case, the app reads the existing batch of notifications in the store and handle any new incoming notifications or notification updates after that
- (void)forceRead {
    NSLog(@"ME123 Forced to read!");
    [self.reader readBatchAsyncWithMaxSize:NSUIntegerMax completion:^(NSArray<MCDUserNotification *> * _Nullable notifications, NSError * _Nullable error) {
        if (error) {
            NSLog(@"ME123 Failed to read batch with error %@", error);
        } else {
            [self _handleNotifications:notifications];
            NSLog(@"ME123 Have %ld listeners", self.listenerMap.count);
            for (void (^listener)(void) in self.listenerMap.allValues) {
                NSLog(@"ME123 Calling a listener about an update!");
                listener();
            }
        }
    }];
}

```
## Update the state of an existing MCDUserNotification
In the previous section, we mentioned that sometimes a MCDUserNotification change received through the reader could be a state update on an existing MCDUserNotification – whether that’s being marked as dismissed or marked as read. In this case, the app client can choose what to do, such as enabling universal dismiss by removing the corresponding visual notification on this particular device. 
Taking a step back, your app client is often the one that initiated this MCDUserNotification change update to begin with – from a different device. You can choose the time to update the state of your MCDUserNotifications, but usually they get updated when the corresponding visual notification is handled by the user on that device, or the notification is further handled by the user in some in-app experience you enable. 
Here is an example of what the flow would look like:
Your app server publishes a notification targeted at User A. User A receives this notification on both his PC and his phone where the app clients are installed. The user clicks on the notification on PC, and chases into the app to handles the corresponding task. The app client on this PC will then call into Connected Devices Platform SDK to update the state of the corresponding User Notification in order to have this update synced across all this user’s devices. The other app clients, upon receiving this state update in real-time, will then remove the corresponding visual alert / message / toast notification from the device’s notification center / notification tray / Action Center. This is how notifications get universally dismissed across a user’s devices. 

> [!TIP] 
> MCDUserNotification class currently provides 2 types of state updates – you can modify the MCDUserNotificationReadState or the MCDUserNotificationUserActionState and define your own logic on what should happen when notifications are updated. For example, you can mark the action state to be Activated or Dismissed, and pivot on that value to implement universal dismiss. Alternatively, or at the same time, you can mark read state as Read or Unread and based on that determine which notifications should show up in the in-app notification history view. 

```ObjectiveC
- (void)dismissNotification:(MCDUserNotification*)notification {
    @synchronized (self) {
        notification.userActionState = MCDUserNotificationUserActionStateDismissed;
        [notification saveAsync:^(__unused MCDUserNotificationUpdateResult * _Nullable result, __unused NSError * _Nullable err) {
            NSLog(@"ME123 Dismiss notification with result %d error %@", result.succeeded, err);
        }];
    }
}

```
