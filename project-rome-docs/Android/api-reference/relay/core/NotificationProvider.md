---
title: NotificationProvider
description: This interface enables an app to become a notification provider to remote apps.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# NotificationProvider interface

```
public interface NotificationProvider
```

This interface enables an app to become a notification provider to remote apps.

## Methods

### getNotificationRegistrationAsync
`@NonNull AsyncOperation<NotificationRegistration> getNotificationRegistrationAsync()`

This method is called when the platform is initialized. The platform queries the app for its notification registration.

#### Returns
An asynchronous operation with the notification registration.

### addNotificationProviderChangedListener
`long addNotificationProviderChangedListener(@NonNull EventListener<NotificationProvider, NotificationRegistration> listener);`

This method is called when the system attempts to add a listener for the "notification provider changed" event.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
A unique identifier for this event listener's registration (needed for removing the listener).

### removeNotificationProviderChangedListener
`void removeNotificationProviderChangedListener(long eventRegistrationToken);`

This method is called when the system attempts to removed a listener for the "notification provider changed" event.

#### Parameters
* `eventRegistrationToken` The unique identifier for the original event listener registration.