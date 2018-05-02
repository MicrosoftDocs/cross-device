---
title: UserActivityContentInfo
description: This class provides basic user activity information that is convertible to a JSON string format.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivityContentInfo class

```
public final class UserActivityContentInfo
```

This class provides basic user activity information that is convertible to a JSON string format.

## Constructors

### fromJson
`public static UserActivityContentInfo fromJson(@NonNull String contentInfo)`

Creates an instance of this class from a JSON string.

#### Parameters
* `contentInfo` The JSON string from which to create this instance.

## Methods

### toJson
`public String toJson()`

Converts this activity info into a JSON-formatted String

#### Returns
The JSON String.
