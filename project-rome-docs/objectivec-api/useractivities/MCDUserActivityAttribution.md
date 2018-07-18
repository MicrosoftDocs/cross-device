---
title: MCDUserActivityAttribution
description: This class manages the graphical elements of a user activity. 
keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
---

# class `MCDUserActivityAttribution`

```
@interface MCDUserActivityAttribution : NSObject
```

This class manages the graphical elements of a user activity.

## Properties

### iconUri
`@property(nonatomic, copy, nonnull) NSString* iconUri;`

The URI for the icon image.

### alternateText
`@property(nonatomic, copy, nonnull) NSString* alternateText;`

The text that describes the icon image (for use with screen readers).


### addImageQuery
`@property(nonatomic, assign) BOOL addImageQuery;`

Determines whether to allow Windows to append a query string to the image URI supplied from **IconUri** when retrieving the image. The query string includes information that can help select the ideal image based on the DPI of the user's display, the high contrast setting, and the user's language. This query string specifies scale, contrast setting, and language; for instance, an **IconUri** value of "www.website.com/images/hello.png" becomes "www.website.com/images/hello.png?ms-scale=100&ms-contrast=standard&ms-lang=en-us".


