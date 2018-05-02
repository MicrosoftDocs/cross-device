---
title: RemoteSystemStatus
description: Contains values that describe the availability of a remote system.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystemStatus enum
```
public enum RemoteSystemStatus
```

Contains values that describe the availability of a remote system. Descriptive values are only given for Windows systems. Other platforms with always show **UNKNOWN**.

|Name | Value | Description |
|--------------------------------|--------------------------------|------------|
|UNAVAILABLE  | 0 | The remote system is reported as unavailable.|
|DISCOVERING_AVAILABILITY | 1 | The status of the remote system is being determined.|
|AVAILABLE | 2 | The remote system is reported as available.|
|UNKNOWN | 3 | The status is unknown.|

