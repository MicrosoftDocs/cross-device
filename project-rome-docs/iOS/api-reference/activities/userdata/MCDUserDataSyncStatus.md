---
title: MCDUserDataSyncStatus
description: Contains values that describe the state of a **[MCDUserDataFeed](MCDUserDataFeed.md)**'s synchronization with the Connected Devices Platform backend. 
keywords: microsoft, windows, user activities, how-to iOS, how-to iPhone 
---

# enum `MCDUserDataSyncStatus`

```
typedef NS_ENUM(NSInteger, MCDUserDataSyncStatus)
```

Contains values that describe the state of a **[MCDUserDataFeed](MCDUserDataFeed.md)**'s synchronization with the Connected Devices Platform backend. 

|Name | Value | Description |
|:-- |:-- |:-- |
|  Queued |0| The data is not yet synchronized. |
| Synchronized |1| The data has been synchronized.|