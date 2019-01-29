---
title: MCDRemoteLaunchUriStatus
description: Contains values that describe the status of a remote app launch using a URI.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDRemoteLaunchUriStatus`

`typedef NS_ENUM(NSInteger, MCDRemoteLaunchUriStatus)`

Contains values that describe the status of a remote app launch using a URI.


| Name    |Value   |Description   |                  
|------ |------- |--|
|MCDRemoteLaunchUriStatusUnknown | 0| The status is unknown.|
|MCDRemoteLaunchUriStatusSuccess | 1| The remote launch was successful.|
|MCDRemoteLaunchUriStatusAppUnavailable | 2 | The target app is unavailable.|
|MCDRemoteLaunchUriStatusProtocolUnavailable | 3 | The target app does not support this URI.|
|MCDRemoteLaunchUriStatusRemoteSystemUnavailable | 4 | The device to which the message was sent is unavailable.|
|MCDRemoteLaunchUriStatusValueSetTooLarge | 5 | The data bundle sent to the target app was too large.|
|MCDRemoteLaunchUriStatusDeniedByLocalSystem | 6 | The client system has prevented use of the Remote Systems Platform.|
|MCDRemoteLaunchUriStatusDeniedByRemoteSystem | 7 | The target device has prevented use of the Remote Systems Platform.|