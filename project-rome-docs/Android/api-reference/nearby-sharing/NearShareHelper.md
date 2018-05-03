---
title: NearShareHelper 
description: This class generates an implementer of the [NearShareFileProvider](NearShareFileProvider.md) interface, which represents a single file to be shared.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareHelper class

```
public class NearShareHelper
```

This class generates an implementer of the [NearShareFileProvider](NearShareFileProvider.md) interface, which represents a single file to be shared.

## Methods

### createNearShareFileFromContentUri
`public static NearShareFileProvider createNearShareFileFromContentUri(Uri contentUri, Context context) throws IllegalArgumentException`

Creates a new implementer of [NearShareFileProvider](NearShareFileProvider.md) with an associated file.

#### Parameters
* `contentUri` A URI pointing to the file to be shared. The returned class will parse this file to deliver the necessary data.
* `context` The application context.

#### Returns
A class instance implementing the [NearShareFileProvider](NearShareFileProvider.md) interface.