---
title: NotificationRegistration
description: TBD
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# NotificationRegistration class

```
public final class NotificationRegistration
```

TBD


## Constructors

### NotificationRegistration
`public NotificationRegistration(@NonNull NotificationType type, @NonNull String token, @Nullable String senderId, @Nullable String displayName)`

Creates a new instance of this class with the given notification type, token, app ID, and app name.

#### Parameters
* `type` TBD
* `token`
* `senderId`
* `displayName`

#### Returns
A new instance of this class.

> Note: Apps that use Google Cloud Messaging notifications (NotificationType value **GCM**) will not be able to send or receive push notifications for users in China.


## Methods

### getNotificationType
`public NotificationType getNotificationType()`

TBD

#### Returns
tbd

### getToken
`public String getToken()`

TBD

#### Returns
tbd

### getApplicationId
`public String getApplicationId()`

TBD

#### Returns
tbd

### getApplicationDisplayName
`public String getApplicationDisplayName()`

TBD

#### Returns
tbd
