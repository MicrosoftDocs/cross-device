---
title: MCDRemoteSystemWatcherError
description: Contains values that the describe an error encountered by a remote system watcher object.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# enum `MCDRemoteSystemWatcherError`

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemWatcherError)
```

Contains values that the describe an error encountered by a remote system watcher object.

|Name | Value | Description |
|:-- |:-- |:-- |
|MCDRemoteSystemWatcherErrorUnknown |0| The watcher encountered an unknown error.|
|MCDRemoteSystemWatcherErrorInternetNotAvailable|1| The watcher failed because the Internet connection was lost.|
|MCDRemoteSystemWatcherErrorAuthenticationError|2| The watcher failed because the system was not authorized to discover remote systems.|