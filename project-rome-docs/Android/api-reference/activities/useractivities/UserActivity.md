---
title: UserActivity
description: This class represents a single user activity instance.
keywords: microsoft, windows, user activities, Android, Android api reference 
---

# UserActivity class

```
public final class UserActivity
```

This class represents a single user activity instance. A user activity is created by an app during its execution to notify the system of a user work stream that can be continued on another device or at another time on the same device. It provides information about a task the user is engaged in.

>**Note:** UserActivity instances have a size limit of 100KB, above which they cannot be published.

## Methods

### getActivityId
`public String getActivityId()`

Gets the unique ID for this activity.

#### Returns
The ID String.

### getState
`public UserActivityState getState()`

Gets the state of this activity.

#### Returns
A [UserActivityState](UserActivityState.md) value describing the state.

### setContentUri
`public void setContentUri(@Nullable String contentUri)`

Sets the content URI for this activity (the URI of the image that will be used to represent the activity on another device).

### getContentUri
`public String getContentUri()`

Gets the content URI for this activity.

### setFallbackUri
`public void setFallbackUri(@Nullable String fallbackUri)`

Sets the web-friendly URI for this activity, to be used if the primary URI fails.

#### Parameters
* `fallbackUri` The fallback URI String.

### getFallbackUri
`public String getFallbackUri()`

Gets the fallback URI held by this activity.

#### Returns
The fallback URI string.

### setContentType
`public void setContentType(@Nullable String contentType)`

Sets the MIME (Multipurpose Internet Mail Extensions) type of the content stored with **setContentUri**. For example, "text/plain".

#### Parameters
* `contentType` The content type String.

### getContentType
`public String getContentType()`

Gets the content type for this activity.

#### Returns
The content type String.

### setActivationUri
`public void setActivationUri(@NonNull String activationUri)`

The URI to follow when this user activity is activated.

#### Parameters
* `activationUri` The primary URI String.

### getActivationUri
`public String getActivationUri()`

Gets the primary URI for this activity.

#### Returns
The primary URI String.

### setContentInfo
`public void setContentInfo(@Nullable UserActivityContentInfo contentInfo)`

Sets the basic content info for this activity. For example, if your activity was reading an RSS feed, the content might include the name of the article and its author.

### getContentInfo
`public UserActivityContentInfo getContentInfo()`

Gets the basic content info for this activity.

### setVisualElements
`public void setVisualElements(@NonNull UserActivityVisualElements visualElements)`

Sets the visual elements for this activity (information that can be used for the "details" tile of the activity).

### getVisualElements
`public UserActivityVisualElements getVisualElements()`

Gets the visual elements for this activity.

### saveAsync
`public AsyncOperation<Void> saveAsync()`

Publishes the user activity. The UserActivity must have an activation URI and a VisualElements member with set display text before this method is called. This method should be called whenever the app modifies a property of the UserActivity (in order to publish the update).

### createSession
`public UserActivitySession createSession()`

Creates a user activity session that this UserActivity will be associated with. An associated UserActivitySession indicates that the user is currently engaged in the activity.
