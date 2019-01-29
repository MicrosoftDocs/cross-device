---
title: MCDConnectedDevicesNotificationRegistration
description: This class represents the app's registration with a push notification service (necessary for some Project Rome scenarios). 
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesNotificationRegistration` 

```
@interface MCDConnectedDevicesNotificationRegistration : NSObject
```  
 This class represents the app's registration with a push notification service (necessary for some Project Rome scenarios). It conveys this information to the Connected Devices Platform.

## Properties

### type
`@property(nonatomic, readwrite) MCDConnectedDevicesNotificationType type;`

The type of notifications in this setup.

### token
`@property(nonatomic, readwrite, nonnull) NSString* token;`

The registration token.

### appId
`@property(nonatomic, readwrite, nonnull) NSString* appId;`

The app ID for push notification registration.

### appDisplayName
`@property(nonatomic, readwrite, nonnull) NSString* appDisplayName;`

The app display name. This should be the name of the app that was used for registration
on the Microsoft dev portal.