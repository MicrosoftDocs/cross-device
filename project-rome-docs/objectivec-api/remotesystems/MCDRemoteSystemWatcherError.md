---
title: MCDRemoteSystemWatcherError
description:   Contains values that the describe an error encountered by a remote system watcher object during
 the discovery process.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDRemoteSystemWatcherError` 

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemWatcherError)
```  
 Contains values that the describe an error encountered by a remote system watcher object during
 the discovery process.

## Fields

| Name                              | Value | Description                    |
|:----------------------------------|:------|:-------------------------------|
| MCDRemoteSystemWatcherErrorUnknown | 0 | The watcher encountered an unknown error. |
| MCDRemoteSystemWatcherErrorInternetNotAvailable | 1 | The error occurred because the Internet connection was lost. |
| MCDRemoteSystemWatcherErrorAuthenticationError | 2 | The error occurred because a ConnectedDevicesAccount being used to run the discovery could not be authenticated. | 
