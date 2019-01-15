---
title: MCDRemoteSystemDiscoveryType
description:  Contains values that describe how remote systems are able to be discovered.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDRemoteSystemDiscoveryType` 

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemDiscoveryType)
```  

Contains values that describe how remote systems are able to be discovered. 

## Fields

| Name                              | Value | Description                    |
|:----------------------------------|:------|:-------------------------------|
| MCDRemoteSystemDiscoveryTypeAny   | 0     | Remote systems are discoverable through any connection.  |
| MCDRemoteSystemDiscoveryTypeProximal | 1     | Remote systems are only discoverable through a proximal connection, such as a local
network or Bluetooth connection. |
| MCDRemoteSystemDiscoveryTypeCloud | 2     | Remote systems are only discoverable through cloud connection. |
| MCDRemoteSystemDiscoveryTypeSpatiallyProximal | 3     | Remote systems are discoverable through a proximal connection and are expected to be
spatially near to the client device (in Bluetooth range, for example).  |

