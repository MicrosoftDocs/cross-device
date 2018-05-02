---
title: UserActivityVisualElements
description: This class contains the visual information, such as the description and icon, that can be shown in the "details" tile for a UserActivity.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivityVisualElements

```
public final class UserActivityVisualElements
```

This class contains the visual information, such as the description and icon, that can be shown in the "details" tile for a UserActivity.

## Methods

### setDisplayText
`public void setDisplayText(@NonNull String displayText)`

Sets the display text for the "details" tile of the activity.

#### Parameters
* `displayText` The display text.

### getDisplayText
`public String getDisplayText()`

Gets the display text for the activity.

#### Returns
The display text.

### setDescriptionText
`public void setDescriptionText(@Nullable String description)`

Sets the description text for the "details" tile of the activity.

#### Parameters
* `description` The description text.

### getDescriptionText
`public String getDescriptionText()`

gets the description text for the activity.

#### Returns
The description text.

### setAttribution
`public void setAttribution(@Nullable UserActivityAttribution attribution)`

Sets graphical information about the activity.

#### Parameters
* `attribution` The [UserActivityAttribution](UserActivityAttribution.md) to set.

### getAttribution
`public UserActivityAttribution getAttribution() `

Gets the graphical information for the activity.

#### Returns
The associated [UserActivityAttribution](UserActivityAttribution.md).

### setContent
`public void setContent(@Nullable String content)`

Sets the content text for the "details" tile of the activity.

#### Parameters
* `content` The content String.

### getContent
`public String getContent()`

Gets the content text for the activity.

#### Returns
The content String.

### setAttributionDisplayText
`public void setAttributionDisplayText(@Nullable String attributionDisplayText)`

Sets the text that is shown in the top banner of the activity card.

#### Parameters
* `attributionDisplayText` The banner text String.

### getAttributionDisplayText
`public String getAttributionDisplayText()`

Gets the text for the top banner of the activity card.

#### Returns
The banner text String.