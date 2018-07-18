---
title: MCDUserActivityContentInfo
description: This class provides basic user activity information that is convertible to a JSON string format.
keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
---

# class `MCDUserActivityContentInfo`

```
@interface MCDUserActivityContentInfo : NSObject
```

This class provides basic user activity information that is convertible to a JSON string format.

## Constructors

### fromJson
`+ (nullable instancetype)fromJson:(nonnull NSString*)contentInfo;`

Creates an instance of this class from a JSON string.

#### Parameters
* `contentInfo` The JSON string from which to create this instance.

#### Returns
A new instance of this class.

## Methods

### toJson
`- (nonnull NSString*)toJson;`

Converts this activity info into a JSON-formatted String

#### Returns
The JSON string.
