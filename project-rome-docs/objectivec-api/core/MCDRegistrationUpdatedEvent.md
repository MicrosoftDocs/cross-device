---
title: MCDRegistrationUpdatedEvent
description:  This class notifies all listeners from the connected devices framework that the notification registration has changed.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRegistrationUpdatedEvent`

```
@interface MCDRegistrationUpdatedEvent : NSObject
```

## Methods

### raiseWithNotificationRegistration
`-(void)raiseWithNotificationRegistration : (nonnull MCDNotificationRegistration*)notificationRegistration;`

Raises an event indicating that the notification registration has changed.

#### Parameters
* `notificationRegistration` The new notification registration.