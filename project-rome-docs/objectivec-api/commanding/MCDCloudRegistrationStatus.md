---
title: MCDCloudRegistrationStatus
description:  Contains values that describe the status of a remote application's registration with the Connected Devices Platform backend.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDCloudRegistrationStatus`

```
typedef NS_ENUM(NSInteger, MCDCloudRegistrationStatus)
```

Contains values that describe the status of a remote application's registration with the Connected Devices Platform backend.

|Name         | Value  | Description    |                           
|--------|-------------|-----|
|MCDCloudRegistrationStatusNotStarted |0| Cloud registration has not started.|
|MCDCloudRegistrationStatusInProgress |1| Cloud registration is in progress.|
|MCDCloudRegistrationStatusSucceeded |2| Cloud registration has succeeded.|
|MCDCloudRegistrationStatusFailed |3| Cloud registration has failed.|