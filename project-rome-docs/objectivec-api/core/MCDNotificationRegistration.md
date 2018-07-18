---
title: MCDNotificationRegistration
description: This class represents the app's registration with a push notification service (necessary for some Project Rome scenarios). 
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDNotificationRegistration`

```
@interface MCDNotificationRegistration : NSObject
```


This class represents the app's registration with a push notification service (necessary for some Project Rome scenarios). It conveys this information to the Connected Devices Platform.

## Properties

### type
`@property(nonatomic, readonly) MCDNotificationType type;`

A [MCDNotificationType](MCDNotificationType.md) value describing the platform type.

> Note: Apps that use Google Cloud Messaging notifications (NotificationType value **GCM**) will not be able to send or receive push notifications for users in China.

### token
`@property(nonatomic, readonly, nonnull) NSString* token;`

The NSData that APN service sends to your app delegate's didRegisterForRemoteNotificationsWithDeviceToken: method.

### applicationId
`@property(nonatomic, readonly, nonnull) NSString* applicationId;`

The app's bundle identifier. 

### applicationDisplayName
`@property(nonatomic, readonly, nonnull) NSString* applicationDisplayName;`

The name of the app that was used for registration on the Microsoft dev portal.

## Constructors

### registrationWithNotificationType
`+ (nullable instancetype)registrationWithNotificationType:(MCDNotificationType)notificationType
    token:(nonnull NSString*)token
    appId:(nonnull NSString*)appId
    appDisplayName:(nonnull NSString*)appDisplayName;`

Creates a new instance of this class with the given notification type, token, app ID, and app name.

#### Parameters
* `notificationType` A [MCDNotificationType](MCDNotificationType.md) value describing the platform type.
* `token` The NSData that APN service sends to your app delegate's didRegisterForRemoteNotificationsWithDeviceToken: method. You must convert the NSData into a string by hex-encoding it.
* `appId` The app's bundle identifier.
* `appDisplayName` The name of the app that was used for registration on the Microsoft dev portal.

### initWithNotificationType
`- (nullable instancetype)initWithNotificationType:(MCDNotificationType)notificationType
    token:(nonnull NSString*)token
    appId:(nonnull NSString*)appId
    appDisplayName:(nonnull NSString*)appDisplayName;`

Creates a new instance of this class with the given notification type, token, app ID, and app name.

#### Parameters
* `notificationType` A [MCDNotificationType](MCDNotificationType.md) value describing the platform type.
* `token` The NSData that APN service sends to your app delegate's didRegisterForRemoteNotificationsWithDeviceToken: method. You must convert the NSData into a string by hex-encoding it.
* `appId` The app's bundle identifier.
* `appDisplayName` The name of the app that was used for registration on the Microsoft dev portal.
