---
title: NearShareStatus 
description: Contains values that describe the result of a nearby sharing operation.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareStatus enum

```
public enum NearShareStatus
```

Contains values that describe the result of a nearby sharing operation.

|Member   |Value   |Description   |
|:--------|:-------|:-------------|
|UNKNOWN |0 | The status is unknown. |
|COMPLETED |1 | The sharing operation comleted. |
|IN_PROGRESS |2 | The sharing operation is still in progress. |
|TIMED_OUT |3 | The sharing operation timed out. |
|CANCELLED |4 | The sharing operation was cancelled. |
|DENIED_BY_REMOTE_SYSTEM |5 | The sharing operation was denied by the receiving device.|
|VERSION_MISMATCH |6 | The operation could not complete because of a version mismatch.|
|CONNECTION_ESTABLISHED |7 | A connection to the receiving device was established.|
|NO_SIGNEDIN_USER |8 | There is not signed in user on the receiving device.|
|NETWORK_ERROR |9 | The operation could not complete because of a network error.|
|PLATFORM_ERROR |10 | The operation could not complete because of a platform error.|
