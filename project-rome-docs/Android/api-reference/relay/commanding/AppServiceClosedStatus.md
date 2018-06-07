---
title: AppServiceConnectionClosedStatus 
description: Contains the values that describe the reason that an app service connection was closed.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# AppServiceConnectionClosedStatus enum

```
public enum AppServiceClosedStatus
```

Contains the values that describe the reason that an app service connection was closed.

>**Important:** Currently, only a value of **UNKNOWN** will be encountered by Android apps.

|Member   |Value   |Description   |
|:--------|:-------|:-------------|
|COMPLETED |0 | The app service connection was closed intentionally by the client app. |
|CANCELLED |1 | The app service connection was closed due to network failure. |
|RESOURCE_LIMITS_EXCEEDED |2 | The app service connection exceeded its allotted program memory. |
|UNKNOWN |3 | The app service connection closed for an unknown reason.|
