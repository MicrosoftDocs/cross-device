---
title: NotificationRegistration
description: This class represents the app's registration with a push notification service (necessary for some Project Rome scenarios). 
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# NotificationRegistration class

```
public final class NotificationRegistration
```

This class represents the app's registration with a push notification service (necessary for some Project Rome scenarios). It conveys this information to the Connected Devices Platform.


## Constructors

### NotificationRegistration
`public NotificationRegistration(@NonNull NotificationType type, @NonNull String token, @Nullable String senderId, @Nullable String displayName)`

Creates a new instance of this class with the given notification type, token, app ID, and app name.

#### Parameters
* `type` A [NotificationType](NotificationType.md) value describing the platform type.
* `token` The string that the messaging service sends to your registration intent service.
* `senderId` The numeric Sender ID that you received when you registered your app for push notifications. 
* `displayName` The app display name. This should be the name of the app that was used for registration on the Microsoft dev portal.

#### Returns
A new instance of this class.

> Note: Apps that use Google Cloud Messaging notifications (NotificationType value **GCM**) will not be able to send or receive push notifications for users in China.


## Methods

### getNotificationType
`public NotificationType getNotificationType()`

Gets the type of notifications in this setup.

#### Returns
The type of notifications in this setup.

### getToken
`public String getToken()`

Gets the registration token.

#### Returns
The registration token.

### getApplicationId
`public String getApplicationId()`

Gets the app ID for push notification registration

#### Returns
The app ID.

### getApplicationDisplayName
`public String getApplicationDisplayName()`

Gets the app display name. This should be the name of the app that was used for registration on the Microsoft dev portal.

#### Returns
The app display name.
