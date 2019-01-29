---
title: MCDRemoteSystemStatus
description:  Contains values that describe the availability of a remote system.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDRemoteSystemStatus` 

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemStatus)
```  
Contains values that describe the availability of a remote system. On iOS apps, a value of **MCDRemoteSystemStatusUnknown** will always be encountered; other values are only available on Windows systems.

## Fields

| Name                              | Value | Description                    |
|:----------------------------------|:------|:-------------------------------|
| MCDRemoteSystemStatusUnavailable | 0 | The remote system is reported as unavailable. |
| MCDRemoteSystemStatusDiscoveringAvailablilty | 1 | The status of the remote system is being determined (occurs during the discovery process). |
| MCDRemoteSystemStatusAvailable | 2 | The remote system is reported as available. |
| MCDRemoteSystemStatusUnknown | 3 | The status is unknown. |
