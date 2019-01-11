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
`@property(nonatomic, copy, nullable) NSString* descriptionText;`

The description text for the "details" tile of the activity.

### backgroundColor
`@property(nonatomic, copy, nullable) SKColor* backgroundColor;`

The background color for the tile of the activity.

### attribution
`@property(nonatomic, retain, nullable) MCDUserActivityAttribution* attribution;`

The graphical information about the activity.

### adaptiveCardJson
`@property(nonatomic, copy, nullable) NSString* adaptiveCardJson;`

The content text for the "details" tile of the activity.

### attributionDisplayText
`@property(nonatomic, copy, nullable) NSString* attributionDisplayText;`

The text that is shown in the top banner of the activity card.