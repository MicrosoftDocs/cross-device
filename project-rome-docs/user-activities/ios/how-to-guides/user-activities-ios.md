---
title: Publishing and reading User Activities (iOS)
description: This guide shows how to create, publish, and read Windows-based User Activities in your iOS app.
ms.author: pafarley
author: PatrickFarley
ms.date: 07/17/2018
ms.topic: article
ms.prod: windows
ms.technology: connected-devices
keywords: microsoft, windows, project rome, user activities, ios
ms.assetid: 445f1dd4-f3c7-46e4-a7cd-42a1fb411172
ms.localizationpriority: medium
---

# Publishing and reading User Activities (iOS)

User Activities are data constructs that represent a user's tasks within an application. They make it possible to save a snapshot of a current task to be continued at a later time. The [Windows Timeline](https://blogs.windows.com/windowsexperience/2018/04/27/make-the-most-of-your-time-with-the-new-windows-10-update/) feature presents Windows users with a scrollable list of all their recent activities, represented as cards with text and graphics. For more information about User Activities in general, see [Continue user activity, even across devices](https://docs.microsoft.com/windows/uwp/launch-resume/useractivities). For recommendations on when to create or update Activities, see the [User Activities best practices](https://docs.microsoft.com/windows/uwp/launch-resume/useractivities-best-practices) guide.

With the Project Rome SDK, your iOS app can not only publish User Activities for use in Windows features such as Timeline, but it can also act as an endpoint and read Activities back to the user just as Timeline does. This allows cross-device apps to completely transcend their platforms and present experiences that follow users rather than devices.

See the [API reference](../api-reference/index.md) page for links to the reference docs relevant to these scenarios.

First, you must initialize the Connected Devices Platform. If you've done this already, skip to the next section.

[!INCLUDE [ios/platform-init](../../../includes/ios/platform-init.md)]

Next, you must enable your app to receive push notifications. If you've done this already, skip to the next section.

[!INCLUDE [ios/notification-init](../../../includes/ios/notification-init.md)]

## Initialize a User Activity channel

To implement User Activity features in your app, you will first need to initialize the user activity feed by creating a **MCDUserActivityChannel**. You should treat this like the Platform initialization step above: it should be checked and possibly redone whenever the app comes to the foreground (but not before Platform initialization). 

You will need a signed-in user account for this step. As above, you may use a class from the [authentication provider sample](https://github.com/Microsoft/project-rome/tree/master/iOS/samples/account-provider-sample) to easily acquire the **MCDUserAccount**(s). You will also need your cross-platform app ID, which was retrieved through the Microsoft Developer Dashboard registration.

The following method from the sample app initializes an **MCDUserActivityChannel**.

```ObjectiveC
// You must be logged in to use UserActivities
NSArray<MCDUserAccount*>* accounts = [[AppDataSource sharedInstance].accountProvider getUserAccounts];
if (accounts.count > 0)
{
    // Get a UserActivity channel, getting the default channel        
    NSLog(@"Creating UserActivityChannel");
    NSArray<MCDUserAccount*>* accounts = [[AppDataSource sharedInstance].accountProvider getUserAccounts];
    MCDUserDataFeed* userDataFeed = [MCDUserDataFeed userDataFeedForAccount:accounts[0]
        platform:[AppDataSource sharedInstance].platform
        activitySourceHost:CROSS_PLATFORM_APP_ID];
    NSArray<MCDSyncScope*>* syncScopes = @[ [MCDUserActivityChannel syncScope] ];
    [userDataFeed addSyncScopes:syncScopes];
    self.channel = [MCDUserActivityChannel userActivityChannelWithUserDataFeed:userDataFeed];
}
else
{
    NSLog(@"Must have an active account to publish activities!");
    self.createActivityStatusField.text = @"Need to be logged in!";
}
```

At this point, you should have an **MCDUserActivityChannel** reference in `channel`.

## Create and publish a User Activity

The following sample code shows how a new **MCDUserActivity** instance is created.

```ObjectiveC
- (IBAction)createActivityButton:(id)sender
{
    // Step #2: Create a UserActivity
    [self.channel getOrCreateUserActivityAsync:[[NSUUID UUID] UUIDString]
        completion:^(MCDUserActivity* activity, NSError* error) {
            if (error)
            {
                NSLog(@"%@", error);
                self.createActivityStatusField.text = @"Error creating activity!";
            }
            else if (!activity)
            {
                NSLog(@"No activity created!");
            }
            else
            {
                dispatch_async(dispatch_get_main_queue(), ^{
                    self.activity = activity;

                    // Create an activityId so the app knows so you know how to get back
                    self.activityId.text = activity.activityId;
                    self.createActivityStatusField.text = @"Created by iOSSample";
                    // Create a deep link so the app can get right back to where it was
                    self.activationUri.text = @"roman-app:";
                    self.createActivityStatusField.text = @"Activity created";
                });
            }
        }];
}
```

In the next method, the visual data of the **MCDUserActivity** is set before the Activity is published. The activation URI will determine what action is taken when the Activity is activated (when it is selected in Timeline, for example). The display text will be shown on other devices when they view the Activity (in Windows Timeline, for example). The iconUri is a web link to an icon image.


```ObjectiveC
- (IBAction)publishActivityButton:(id)sender
{
    self.createActivityStatusField.text = @"Saving";
    self.activity.activationUri = self.activationUri.text;
    // Set the display text for your activity.
    self.activity.visualElements.displayText = @"Visual Element, like an Adaptive Card";
    self.activity.visualElements.attribution.iconUri = @"https://www.microsoft.com/favicon.ico";

    // ...
```

Once the **MCDUserActivity** is populated with this data, the publish operation takes place.

```ObjectiveC
    // ...

    // Publish the Activity
    [self.activity saveAsync:^(NSError* error) {
        dispatch_async(dispatch_get_main_queue(), ^{
            if (error)
            {
                NSLog(@"%@", error);
                self.createActivityStatusField.text = @"Error saving activity";
            }
            else
            {
                self.createActivityStatusField.text = @"Saved successfully!";
                [self.sessionButton setTitle:@"Start Session" forState:normal];
            }
        });
    }];
}

mActivityId = UUID.randomUUID().toString();
mDisplayText = "Created by OneSDK Sample App";
mActivationUri = "http://contoso.com");
```
> [!TIP] 
> In addition to the properties above, there are many other features that can be configured. For a complete look at the different ways that a UserActivity can be customized, see the **[MCDUserActivity](../../../objectivec-api/useractivities/MCDUserActivity.md)**, **[MCDUserActivityVisualElements](../../../objectivec-api/useractivities/MCDUserActivityVisualElements.md)**, and **[MCDUserActivityAttribution](../../../objectivec-api/useractivities/MCDUserActivityAttribution.md)** classes. See the [User Activities best practices](https://docs.microsoft.com/windows/uwp/launch-resume/useractivities-best-practices) guide for detailed recommendations on how to design User Activities.

## Update an existing User Activity

If you have an existing activity and wish to update its information (in the event of a new engagement, changed page, and so on), you can do so by using a **MCDUserActivitySession**. 

Once you've created a session, your app can make any desired changes to the properties of the **UserActivity**. When you're done making changes, close the session. 

The following method from the sample app toggles a session on and off.

```ObjectiveC
- (IBAction)manageSessionButton:(id)sender
{

    // Start a new a session for the UserActivity
    if (self.session == nil)
    {
       self.session = [self.activity createSession];
        dispatch_async(dispatch_get_main_queue(), ^{
            NSLog(@"UserActivitySession has started %@", self.session);
            self.session = [self.activity createSession];
            dispatch_async(dispatch_get_main_queue(), ^{ [self.sessionButton setTitle:@"Stop Session" forState:normal]; });
        });
    }
    else
    {
        // Stop the UserActivitySession
        [self.session close];
        self.session = nil;
        dispatch_async(dispatch_get_main_queue(), ^{
            NSLog(@"UserActivitySession has stopped %@", self.session);
            [self.sessionButton setTitle:@"Start Session" forState:normal];
        });
    }
}
```


An **MCDUserActivitySession** can be thought of as a way to create a **MCDUserActivitySessionHistoryItem** (covered in the next section). Rather than create a new **MCDUserActivity** every time a user moves to a new page, you can simply create a new session for each page. This will make for a more intuitive and organized activity reading experience.

## Read User Activities

Your app can read User Activities and present them to the user just as the Windows Timeline feature does. To set up User Activity reading, you use the same **MCDUserActivityChannel** instance from earlier. This instance can expose **MCDUserActivitySessionHistoryItem** instances, which represent a user's engagement in a particular Activity during a specific period of time.

```ObjectiveC
- (IBAction)readActivityButton:(id)sender
{

    // Read/sync your UserActivities
    [self.channel getRecentUserActivitiesAsync:(NSInteger)5
        completion:^(NSArray<MCDUserActivitySessionHistoryItem*>* _Nonnull result, NSError* _Nullable error) {
            dispatch_async(dispatch_get_main_queue(), ^{
                if (error)
                {
                    self.readActivityStatusField.text = @"Error reading activity!";
                }
                else if (result.count == 0)
                {
                    self.readActivityStatusField.text = @"Read completed, no activities returned";
                }
                else
                {
                    self.readActivityStatusField.text = @"Read completed!";
                    MCDUserActivitySessionHistoryItem* item = result.firstObject;
                    self.activityList.text = item.userActivity.activityId;
                    self.activityDisplay.text = item.userActivity.visualElements.displayText;
                }
            });
        }];
}
```

Now your app should have a populated list of **MCDUserActivitySessionHistoryItem**s. Each of these can deliver the underlying **MCDUserActivity** (see **[MCDUserActivitySessionHistoryItem](../../../objectivec-api/useractivities/MCDUserActivitySessionHistoryItem.md)** for details), which you can then display to the user.
