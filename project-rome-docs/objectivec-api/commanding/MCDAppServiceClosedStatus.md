---
title: MCDAppServiceClosedStatus
description:  Contains values that describe a closed connection to a remote app service.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# enum `MCDAppServiceClosedStatus`

```
typedef NS_ENUM(NSInteger, MCDAppServiceClosedStatus)
```

Contains values that describe a closed connection to a remote app service.

|Member   |Value   |Description   |
|--------|-------|-------------|
|MCDAppServiceClosedStatusCompleted |0| The endpoint for the app service closed gracefully.|
|MCDAppServiceClosedStatusCanceled |1| The endpoint for the app service was closed by the client or the system.|
|MCDAppServiceClosedStatusResourceLimitsExceeded |2| The endpoint for the app service was closed because the endpoint ran out of resources.|
|MCDAppServiceClosedStatusUnknown |3| An unknown error occurred.|