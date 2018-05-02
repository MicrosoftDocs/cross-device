---
title: MCDNotificationRegistration
description: TBD
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDNotificationRegistration`

```
@interface MCDNotificationRegistration : NSObject
```

TBD

## Properties

### type
`@property(nonatomic, readonly) MCDNotificationType type;`

TBD

> Note: Apps that use Google Cloud Messaging notifications (NotificationType value **GCM**) will not be able to send or receive push notifications for users in China.

### token
`@property(nonatomic, readonly, nonnull) NSString* token;`

TBD

### applicationId
`@property(nonatomic, readonly, nonnull) NSString* applicationId;`

TBD

### applicationDisplayName
`@property(nonatomic, readonly, nonnull) NSString* applicationDisplayName;`

TBD

## Constructors

### registrationWithNotificationType
`+ (nullable instancetype)registrationWithNotificationType:(MCDNotificationType)notificationType
                                                    token:(nonnull NSString*)token
                                                    appId:(nonnull NSString*)appId
                                           appDisplayName:(nonnull NSString*)appDisplayName;`

Creates a new instance of this class with the given notification type, token, app ID, and app name.

#### Parameters
* `notificationType` TBD
* `token`
* `appId`
* `appDisplayName`

#### Returns
A new instance of this class.

### initWithNotificationType
`- (nullable instancetype)initWithNotificationType:(MCDNotificationType)notificationType
                                            token:(nonnull NSString*)token
                                            appId:(nonnull NSString*)appId
                                   appDisplayName:(nonnull NSString*)appDisplayName;`

Creates a new instance of this class with the given notification type, token, app ID, and app name.

#### Parameters
* `notificationType` TBD
* `token`
* `appId`
* `appDisplayName`

#### Returns
A new instance of this class.

> Note: Apps that use Google Cloud Messaging notifications (NotificationType value **GCM**) will not be able to send or receive push notifications for users in China.
