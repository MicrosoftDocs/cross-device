---
title: Publishing and reading User Activities (iOS)
description: This guide shows how to create, publish, and read Windows-based User Activities in your iOS app.
keywords: microsoft, windows, project rome, iOS api reference 
---

# Publishing and reading User Activities (iOS)

> **Important:** Before you use this guide, make sure you have completed all of the preliminary steps laid out in [Getting started with Connected Devices](getting-started-rome-iOS.md). Additionally, you will need to have completed the "Preliminary setup" section of the [Hosting guide](hosting-iOS.md).

User Activities are data constructs that represent a user's tasks within an application. They make it possible to save a snapshot of a current task to be continued at a later time. The [Windows Timeline](https://blogs.windows.com/windowsexperience/2018/04/27/make-the-most-of-your-time-with-the-new-windows-10-update/) feature presents Windows users with a scrollable list of all their recent activities, represented as cards with text and graphics. For more information about User Activities in general, see [Continue user activity, even across devices](https://docs.microsoft.com/windows/uwp/launch-resume/useractivities).

With the Project Rome SDK, your iOS app can not only publish User Activities for use in Windows features such as Timeline, but it can also act as an endpoint and read Activities back to the user just as Timeline does. This allows cross-device apps to completely transcend their platforms and present experiences that follow users rather than devices.

> Important: As this is a preview release, there are some known bugs in the Project Rome platform. Currently, Windows apps cannot read Activities created by iOS/Android apps, and the same holds true for the reverse. We are working on a timely fix. 

## Initialize a User Activity channel

To implement User Activity features in your app, you will first need to initialize the user activity feed by creating a **MCDUserActivityChannel**. You should treat this like the Platform initialization step in the [Getting started guide](getting-started-rome-iOS.md): it should be checked and possibly re-done whenever the app comes to the foreground. 

The following method from the sample app initializes a **MCDUserActivityChannel**.

```Objective-C
- (void)viewDidLoad
{
    [super viewDidLoad];

    // You must be logged in to use UserActivities
    s_accountProvider = [IdentityViewController accountProvider];
    NSArray<MCDUserAccount*>* accounts = [s_accountProvider getUserAccounts];
    if (accounts.count > 0)
    {
        // Step #1: Get a UserActivity channel, getting the default channel
        self.channel = [MCDUserActivityChannel userActivityChannelWithUserAccount:accounts[0]];
    }
    else
    {
        NSLog(@"Must have an active account to publish activities!");
        self.createActivityStatusField.text = @"Need to be logged in!";
    }
}
```

At this point, you should have a **UserActivityChannel** reference in `channel`.

## Create and publish a User Activity

The following code shows how a new **MCDUserActivity** instance is created in the sample.

```Objective-C
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

In the next method, the visual data of the **MCDUserActivity** is set before the Activity is published. The activationUri will determine what action is taken when the UserActivity is activated (when it is selected in Timeline, for example). The displayText will be shown on other devices when they view the Activity (in Windows Timeline, for example). The iconUri is a web link to an icon image.


```Objective-C
- (IBAction)publishActivityButton:(id)sender
{
    self.createActivityStatusField.text = @"Saving";
    self.activity.activationUri = self.activationUri.text;
    // Set the display text for your activity.
    self.activity.visualElements.displayText = @"Visual Element, like an Adaptive Card";
    self.activity.visualElements.attribution.iconUri = @"https://www.microsoft.com/favicon.ico";

    // ...
```
Once the MCDUserActivity is populated with this data, the publish operation takes place.

```Objective-C
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

For more information on the different ways that a UserActivity can be customized, see the **[MCDUserActivity](../api-reference/activities/useractivities/MCDUserActivity.md)**, **[MCDUserActivityVisualElements](../api-reference/activities/useractivities/MCDUserActivityVisualElements.md)**, and **[MCDUserActivityAttribution](../api-reference/activities/useractivities/MCDUserActivityAttribution.md)** classes.


## Update an existing User Activity

If you have an existing activity and wish to update its information (in the event of a new engagement, changed page, and so on), you can do so by using a **MCDUserActivitySession**. 

Once you've created a session, your app can make any desired changes to the properties of the **UserActivity**. When you're done making changes, close the session. 

The following button method from the sample app toggles a session on and off.

```Objective-C
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


A **MCDUserActivitySession** can be viewed as a way to create a **MCDUserActivitySessionHistoryItem** (covered in the next section). Rather than create a new **MCDUserActivity** every time a user moves to a new page, you can simply create a new session for each page. This will make for a more intuitive and organized activity reading experience.

## Read User Activities

Your app can read User Activities and present them to the user just as the Windows Timeline feature does. To set up User Activity reading, you use the same **MCDUserActivityChannel** as explained at the beginning of this guide. The app receives **MCDUserActivitySessionHistoryItem** instances, which represent a user's engagement in a particular Activity during a specific period of time.

```Objective-C
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

Now your app should have a populated list of **UserActivitySessionHistoryItem**s. Each of these can deliver the underlying **UserActivity** (see [UserActivitySessionHistoryItem](../api-reference/activities/useractivities/UserActivitySessionHistoryItem.md) for details), which you can then display to the user.