---
title: RemoteSystemDiscoveryType
description: Contains values that describe the discovery type of a remote system.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystemDiscoveryType enum

```
public enum RemoteSystemDiscoveryType
```

Contains values that describe the discovery type of a remote system.


|Name | Value | Description |
|:-- |:-- |:-- |
|ANY |0| Remote systems are discoverable through any connection.|
| PROXIMAL|1|Remote systems are only discoverable through a proximal connection, such as a local network or Bluetooth connection.|
| CLOUD|2|Remote systems are only discoverable through cloud connection.|
| SPATIALLY_PROXIMAL|3|Remote systems are discoverable through a proximal connection and are expected to be spatially near to the client device.|
