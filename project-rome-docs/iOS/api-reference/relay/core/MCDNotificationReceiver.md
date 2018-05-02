---
title: MCDNotificationReceiver
description: This class is responsible for receiving push notifications and relaying them into the app.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDNotificationReceiver`

```
@interface MCDNotificationReceiver : NSObject
```

This class is responsible for receiving push notifications and relaying them into the app.

## Methods

### receiveNotification
`+ (BOOL)receiveNotification:(nonnull NSDictionary*)userInfo;`

This method is called when the app receives a push notification; it exposes the notification to the connected devices platform.

#### Parameters
* `userInfo` Information about the user to which the notification was sent. TBD

#### Returns
YES if the connected devices platform processed the notification, NO otherwise.