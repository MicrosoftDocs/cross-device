---
title: MCDUserActivity
description: This class represents a single user activity instance.
keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
---

# class `MCDUserActivity`

```
@interface MCDUserActivity : NSObject
```

This class represents a single user activity instance. A user activity is created by an app during its execution to notify the system of a user work stream that can be continued on another device or at another time on the same device. It provides information about a task the user is engaged in.

>**Note:** MCDUserActivity instances have a size limit of 100KB, above which they cannot be published.

## Properties

### activityId
`@property(nonatomic, readonly, nonnull) NSString* activityId;`

The unique ID for this activity.

### state
`@property(nonatomic, readonly) MCDUserActivityState state;`

The state of this activity.

### contentUri
`@property(nonatomic, copy, nonnull) NSString* contentUri;`

The content URI for this activity (the URI of the image that will be used to represent the activity on another device).

### fallbackUri
`@property(nonatomic, copy, nonnull) NSString* fallbackUri;`

The web-friendly URI held by this activity, to be used if the primary URI fails.

### contentType
`@property(nonatomic, copy, nonnull) NSString* contentType;`

the MIME (Multipurpose Internet Mail Extensions) type of the content stored in **contentUri**. For example, "text/plain".

### activationUri
`@property(nonatomic, copy, nonnull) NSString* activationUri;`

The URI to follow when this user activity is activated.

### contentInfo
`@property(nonatomic, strong, nonnull) MCDUserActivityContentInfo* contentInfo;`

The basic content info for this activity. For example, if your activity was reading an RSS feed, the content might include the name of the article and its author.

### visualElements
`@property(nonatomic, copy, nonnull) MCDUserActivityVisualElements* visualElements;`

The visual elements for this activity (information that can be used for the "details" tile of the activity).

## Methods

### createSession
`- (nonnull MCDUserActivitySession*)createSession;`

Creates a user activity session that this MCDUserActivity will be associated with. An associated MCDUserActivitySession indicates that the user is currently engaged in the activity.

#### Returns
The created session.

### saveAsync
`- (void)saveAsync:(nonnull void (^)(NSError* _Nullable))completionBlock;`

Publishes the user activity. The MCDUserActivity must have an activation URI and a VisualElements member with set display text before this method is called. This method should be called whenever the app modifies a property of the MCDUserActivity (in order to publish the update).

#### Parameters
* `completionBlock` The code block to execute upon completion.

## Example

The following sample code shows how to create and publish a User Activity.

```Objective-C
// In the context of the sample app, this method is called on a button click
- (IBAction)createActivityButton:(id)sender {
    
    // Create a MCDUserActivity:
    // The MCDUserActivityChannel "channel" is created beforehand.
    // A unique ID is generated for the activity ID parameter.
    [self.channel getOrCreateUserActivityAsync:[[NSUUID UUID] UUIDString]
        // handle the method completion (parse the Activity):
        completion:^(MCDUserActivity* activity, NSError* error) {
            if (error) {
                // handle the error in activity creation
                NSLog(@"%@", error);
            }
            else if (!activity) {
                // handle the case of a missing activity
                NSLog(@"No activity created!");
            }
            else {
                dispatch_async(dispatch_get_main_queue(),^{
                    self.activity = activity;
                    
                    // Create an activityId so the app can reference it
                    // in the future.
                    self.activityId.text = activity.activityId;

                    // Create a deep link so the app can get right 
                    // back to where it was
                    self.activationUri.text = @"http://contoso.com";
                });
            }
        }];
}

// Next, attempt to publish the activity.
// In the context of the sample app, this method is called on a button click
- (IBAction)publishActivityButton:(id)sender {
    
    self.activity.activationUri = self.activationUri.text;
    
    // Set the display text for your activity.
    self.activity.visualElements.displayText = @"Visual Element, like an Adaptive Card";
    
    // Publish the Activity
    [self.activity saveAsync:^(NSError* error) {
        dispatch_async(dispatch_get_main_queue(), ^{
            if (error) {
                // handle the publishing error
                NSLog(@"%@", error);
            }
            else {
                // notify the user that the Activity was saved 
                // successfully
            }
        });
    }];
}
```