---
title: MCDConnectedDevicesAccountAddedStatus
description: Learn about the MCDConnectedDevicesAccountAddedStatus enum. This enum contains values that describe the add account operation status.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDConnectedDevicesAccountAddedStatus`

```
typedef NS_ENUM(NSInteger, MCDConnectedDevicesAccountAddedStatus)
```  
Contains the values that describe the add account operation status.

## Fields

| Name                              |   Value     | Description |
|:----------------------------------|:------|:-------------------------------|
| MCDConnectedDevicesAccountAddedStatusSuccess | 0 | The account was successfully added to the platform. |
| MCDConnectedDevicesAccountAddedStatusErrorNoNetwork | 1 | The account operation failed since Rome detected no network access. |
| MCDConnectedDevicesAccountAddedStatusErrorServiceFailed | 2 | The account operation failed since Rome was unable to contact web services. |
| MCDConnectedDevicesAccountAddedStatusErrorNoTokenRequestSubscriber | 3 | The account operation failed since the app didn't subscribe to the AccessTokenRequested event. |
| MCDConnectedDevicesAccountAddedStatusErrorTokenRequestFailed | 4 | The account operation failed since the app failed to return a token when requested. |
| MCDConnectedDevicesAccountAddedStatusErrorUnknown | 5 | The account operation failed for unknown reasons. |
