---
title: RemoteSystemAuthorizationKind
description: Contains values that describe the potential authorization kinds (user-based authorization scopes) of remote systems.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# RemoteSystemAuthorizationKind enum

```
public enum RemoteSystemAuthorizationKind
```

Contains values that describe the potential authorization kinds (user-based authorization scopes) of remote systems.

|Name | Value | Description |
|:-- |:-- |:-- |
|SAME_USER | 0 | The system can only discover and connect with devices signed onto by the same user.|
|ANONYMOUS |1| The system can discover and connect with other users' devices, provided they are in proximity and allow anonymous discovery.|

