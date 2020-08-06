---
title: MCDUserActivity
description: Learn about the MCDUserActivity class and its properties. This class represents a single user activity instance.
keywords: microsoft, windows, user activities, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDUserActivity`

```
@interface MCDUserActivity : NSObject
```

This class represents a single user activity instance. A user activity is created by an app during its execution to notify the system of a user work stream that can be continued on another device or at another time on the same device. It provides information about a task the user is engaged in.

>**Note:** MCDUserActivity instances have a size limit of 100KB, above which they cannot be published.

## Properties

### activityId
`@property(nonatomic, readonly, nonnull) NSString* activityId;`

The unique ID for this activity.

### state
`@property(nonatomic, readonly) MCDUserActivityState state;`

The state of this activity.

### activationUri
`@property(nonatomic, copy, nonnull) NSString* activationUri;`

The URI to follow when this user activity is activated.

### fallbackUri
`@property(nonatomic, copy, nullable) NSString* fallbackUri;`

The web-friendly URI held by this activity, to be used if the primary URI fails.

### contentUri
`@property(nonatomic, copy, nullable) NSString* contentUri;`

The content URI for this activity (the URI of the image that will be used to represent the activity on another device).

### contentType
`@property(nonatomic, copy, nullable) NSString* contentType;`

the MIME (Multipurpose Internet Mail Extensions) type of the content stored in **contentUri**. For example, "text/plain".

### contentInfoJson
`@property(nonatomic, copy, nullable) NSString* contentInfoJson;`

The basic content info for this activity. For example, if your activity was reading an RSS feed, the content string might include the name of the article and its author.

### appDisplayName
`@property(nonatomic, readonly, nullable) NSString* appDisplayName;`

The app display name for this activity.

### visualElements
`@property(nonatomic, retain, nonnull) MCDUserActivityVisualElements* visualElements`

The visual elements for this activity (information that can be used for the "details" tile of the activity).

### roamable
`@property(nonatomic, assign, getter = isRoamable) BOOL roamable;`

Gets or sets whether this activity is roamed to other endpoints.

## Constructors

### activityWithActivityId
`+ (nullable instancetype)activityWithActivityId:(nonnull NSString*)activityId;`

Creates an instance of this class with a given ID.

#### Parameters
* `activityId` 

The identifier for this Activity (should be a unique string).

#### Returns
Returns an instance of this class.

### initWithActivityId
`- (nullable instancetype)initWithActivityId:(nonnull NSString*)activityId;`

Creates an instance of this class with a given ID.

#### Parameters
* `activityId`

The identifier for this Activity (should be a unique string).

#### Returns
Returns an instance of this class.

## Methods

### createSession
`- (nonnull MCDUserActivitySession*)createSession;`

Creates a user activity session that this MCDUserActivity will be associated with. An associated MCDUserActivitySession indicates that the user is currently engaged in the activity.

#### Returns
The created session.

### saveAsync
`- (void)saveAsync:(nonnull void (^)(NSError* _Nullable))completionBlock;`

Publishes the user activity. The MCDUserActivity must have an activation URI and a VisualElements member with set display text before this method is called. This method should be called whenever the app modifies a property of the MCDUserActivity (in order to publish the update).

#### Parameters
* `completionBlock` The code block to execute upon completion.