---
title: NotificationReceiver
description: This class is responsible for receiving push notifications and relaying them into the app.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# NotificationReceiver class

```
public final class NotificationReceiver extends SDKLoader
```

This class is responsible for receiving push notifications and relaying them into the app.

## Methods

### Receive
`public static boolean Receive(@NonNull Bundle bundle)`

This method is called when the app receives a push notification; it exposes the notification to the connected devices platform.

#### Parameters
* `bundle` The notification information.

#### Returns
**true** if the Connected Devices platform processed the notification, **false** if the notification was not associated with the Platform.