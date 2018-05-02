---
title: MCDUserActivitySession
description: This class tracks a user activity ([MCDUserActivity](MCDUserActivity.md) instance) while the user is engaged in that activity.

keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
---

# class `MCDUserActivitySession`

```
@interface MCDUserActivitySession : NSObject
```

This class tracks a user activity ([MCDUserActivity](MCDUserActivity.md) instance) while the user is engaged in that activity.

A [MCDUserActivity](MCDUserActivity.md) is associated with an MCDUserActivitySession which tracks how long the user is engaged in that activity. For example, an activity such as watching a movie can occur on-and-off over the course of multiple days. When the user first starts the new activity of watching a movie, a MCDUserActivitySession must be created. It should be disposed when the user switches to a different activity. When the user resumes, the app should create another **MCDUserActivitySession** from the original [MCDUserActivity](MCDUserActivity.md) to track the activity as long as the user is watching the movie.


## Properties

### activityId
`@property(nonatomic, readonly, nonnull) NSString* activityId;`

A unique ID for this MCDUserActivitySession.

## Methods

### close
`- (void)close;`

Closes this activity session. This should be called when the user is no longer engaged in the activity associated with this session.

## Example

The following sample code uses a MCDUserActivitySession to start or stop an Activity session.

```Objective-C
// In the context of the sample app, this method is called on a button click
- (IBAction)manageSessionButton:(id)sender {
    
    // Start a new a session for the MCDUserActivity
    if (self.session == nil) {
        // use a previously created MCDUserActivity instance to created
        // a MCDUserActivitySession.
        self.session = [self.activity createSession];
        dispatch_async(dispatch_get_main_queue(),^{
            NSLog(@"MCDUserActivitySession has started %@", self.session);
            self.session = [self.activity createSession];
            // change the function of the button pressed to "stop"
            dispatch_async(dispatch_get_main_queue(), ^{
                [self.sessionButton setTitle:@"Stop Session" forState:normal];
            });
        });
    }
    else {
        // Stop the MCDUserActivitySession
        [self.session close];
        self.session = nil;
        dispatch_async(dispatch_get_main_queue(),^{
            NSLog(@"MCDUserActivitySession has stopped %@", self.session);
             // change the function of the button back to "start"
             [self.sessionButton setTitle:@"Start Session" forState:normal];
        });
    }
}
```