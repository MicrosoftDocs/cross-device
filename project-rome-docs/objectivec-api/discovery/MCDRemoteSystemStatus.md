---
title: MCDRemoteSystemStatus
description: Contains values that describe the availability of a remote system.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# enum `MCDRemoteSystemStatus`
```
typedef NS_ENUM(NSInteger, MCDRemoteSystemStatus)
```

Contains values that describe the availability of a remote system. 

## Fields

Name | Value | Description 
--------------------------------|--------------------------------|------------
MCDRemoteSystemStatusUnavailable  | 0 | The status is unknown.
MCDRemoteSystemStatusDiscoveringAvailability | 1 | The status of the remote system is being determined.
MCDRemoteSystemStatusAvailable | 2 | The remote system is reported as available.
MCDRemoteSystemStatusUnknown | 3 | The remote system is reported as unavailable.