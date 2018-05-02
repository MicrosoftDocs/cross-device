---
title: UserActivityAttribution
description: This class manages the graphical elements of a user activity.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivityAttribution class

```
public final class UserActivityAttribution
```

This class manages the graphical elements of a user activity.

## Methods

### setIconUri
`public void setIconUri(@Nullable String iconUri)`

Sets the URI for the icon image.

#### Parameters
* `iconUri` The URI String.

### getIconUri
`public String getIconUri()`

Gets the URI for the icon image.

#### Returns
The URI String.

#### Returns
The URI String.

### setAddImageQuery
`public void setAddImageQuery(boolean addImageQuery)`

Determines whether to allow Windows to append a query string to the image URI supplied from **IconUri** when retrieving the image. The query string includes information that can help select the ideal image based on the DPI of the user's display, the high contrast setting, and the user's language. This query string specifies scale, contrast setting, and language; for instance, an **IconUri** value of "www.website.com/images/hello.png" becomes "www.website.com/images/hello.png?ms-scale=100&ms-contrast=standard&ms-lang=en-us".

#### Parameters 
* `addImageQuery` Set to **true** if your server hosts images and can handle query strings. Otherwise **false**.

### getAddImageQuery
`public boolean getAddImageQuery()`

Gets the image query setting.

#### Returns
**true** if the attribution is set to use query strings, otherwise **false**.

### setAlternateText
`public void setAlternateText(@Nullable String alternateText)`

Sets the text that describes the icon image (for use with screen readers).

#### Parameters
* `alternateText` The alternate text String.

### getAlternateText
`public String getAlternateText()`

Gets the text that describes the icon image.

#### Returns
The alternate text String.