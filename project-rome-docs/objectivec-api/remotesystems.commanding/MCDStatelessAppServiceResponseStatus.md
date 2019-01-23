---
title: MCDStatelessAppServiceResponseStatus
description:  Contains values that describe the status of a message sent from one app service to another
 (whether the message data was successfully delivered).
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# enum `MCDStatelessAppServiceResponseStatus`

`typedef NS_ENUM(NSInteger, MCDStatelessAppServiceResponseStatus)`

 Contains values that describe the status of a message sent from one app service to another
 (whether the message data was successfully delivered).


| Name    |Value   |Description   |                  
|------ |------- |--|
|MCDStatelessAppServiceResponseStatusSuccess | 0| The message was delivered successfully. |
|MCDStatelessAppServiceResponseStatusAppNotInstalled | 1| The package for the app service to which a connection was attempted is not installed on the device. Check that the package is installed before trying to open a connection to theap p service. |
|MCDStatelessAppServiceResponseStatusAppUnavailable | 2 | The package for the app service to which a connection was attempted is temporarily
unavailable. Try to connect again later. |
|MCDStatelessAppServiceResponseStatusAppServiceUnavailable | 3 | The app with the specified package ID is installed and available, but the app does not declare support for the specified app service. Check that the name of the app service and the version of the app are correct. |
|MCDStatelessAppServiceResponseStatusRemoteSystemUnavailable | 4 | The message was not delivered because a connection to the remote device could not be established.|
|MCDStatelessAppServiceResponseStatusRemoteSystemNotSupportedByApp | 5 | The remote app is not configured to support remote connectivity. |
|MCDStatelessAppServiceResponseStatusNotAuthorized | 6 | The app service is not authorized to communicate with the remote device. |
|MCDStatelessAppServiceResponseStatusResourceLimitsExceeded | 7 | The message was not delivered because it exceeded the program memory limits of the remote app service.|
|MCDStatelessAppServiceResponseStatusMessageSizeTooLarge | 8 | The message was not delivered because it exceeded the allowed size. |
|MCDStatelessAppServiceResponseStatusFailure | 9 | The message was not delivered due to network failure. |
|MCDStatelessAppServiceResponseStatusUnknown | 10 |The messaged was not delivered for an unknown reason. |