---
title: MCDAppServiceConnectionStatus
description:  Contains values that describe the status of a connection to a remote app service.  
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# enum `MCDAppServiceConnectionStatus`

```
typedef NS_ENUM(NSInteger, MCDAppServiceConnectionStatus)
```

Contains values that describe the status of a connection to a remote app service. See [Create and consume an app service](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service) for information on app services on Windows devices.

|Name   |Value   |Description   |
|--------|-------|-------------|
|MCDAppServiceConnectionStatusSuccess | 0| The connection to the app service was opened successfully.|
|MCDAppServiceConnectionStatusAppNotInstalled | 1| The package for the app service to which a connection was attempted is not installed on the device. Check that the package is installed before trying to open a connection to the app service.|
|MCDAppServiceConnectionStatusAppUnavailable | 2| The package for the app service to which a connection was attempted is temporarily unavailable. Try to connect again later.|
|MCDAppServiceConnectionStatusAppServiceUnavailable | 3| The app with the specified package ID is installed and available, but the app does not declare support for the specified app service. Check that the name of the app service and the version of the app are correct.|
|MCDAppServiceConnectionStatusUnknown | 4| The connection could not be established for an unknown reason.|
|MCDAppServiceConnectionStatusRemoteSystemUnavailable | 5| The target remote device or application is no longer available for connection.|
|MCDAppServiceConnectionStatusRemoteSystemNotSupportedByApp | 6|The client app is not configured to support remote connectivity.|
|MCDAppServiceConnectionStatusNotAuthorized | 7| The client device is not authorized to support remote connectivity. This may occur because the MCDAppServiceConnection was passed an invalid token.|