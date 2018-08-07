---
title: MCDUserActivityVisualElements
description: This class contains the visual information, such as the description and icon, that can be shown in the "details" tile for a MCDUserActivity.
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserActivityVisualElements`

```
@interface MCDUserActivityVisualElements : NSObject 
```

This class contains the visual information, such as the description and icon, that can be shown in the "details" tile for a MCDUserActivity.

## Properties

### displayText
`@property(nonatomic, copy, nonnull) NSString* displayText;`

The display text for the "details" tile of the activity.

### descriptionText
`@property(nonatomic, copy, nonnull) NSString* descriptionText;`

The description text for the "details" tile of the activity.

### attribution
`@property(nonatomic, copy, nonnull) MCDUserActivityAttribution* attribution;`

The graphical information about the activity.

### adaptiveCardJson
`@property(nonatomic, copy, nonnull) NSString* adaptiveCardJson;`

The content text for the "details" tile of the activity.

### attributionDisplayText
`@property(nonatomic, copy, nonnull) NSString* attributionDisplayText;`

The text that is shown in the top banner of the activity card.


## Example

The following sample code shows how publish a User Activity. It uses a MCDUserActivityVisualElements instance to configure the Activity.

```ObjectiveC
// Attempt to publish the activity.
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