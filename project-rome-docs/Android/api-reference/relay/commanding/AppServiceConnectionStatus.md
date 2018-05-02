---
title: AppServiceConnectionStatus 
description: Contains the values that describe a connection to a remote app service.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# AppServiceConnectionStatus enum
Contains the values that describe a connection to a remote app service.

## Fields

|Member   |Value   |Description   |
|:--------|:-------|:-------------|
|SUCCESS|0|The connection to the app service was opened successfully.|
|APP_NOT_INSTALLED |1 |The package for the app service to which a connection was attempted is not installed on the device. Check that the package is installed before trying to open a connection to the app service. |
|APP_UNAVAILABLE |2 |The package for the app service to which a connection was attempted is temporarily unavailable. Try to connect again later. |
|APPSERVICE_UNAVAILABLE |3 |The app with the specified package ID is installed and available, but the app does not declare support for the specified app service. Check that the name of the app service and the version of the app are correct. |
|UNKNOWN|4 |The connection could not be established for an unknown reason.|
|REMOTE_SYSTEM_UNAVAILABLE |5 |The target remote device or application is no longer available for connection.|
|REMOTE_SYSTEM_NOT_SUPPORTEDBYAPP |6 |The client app is not configured to support remote connectivity. |
|NOT_AUTHORIZED |7 |The client device is not authorized to support remote connectivity. |

