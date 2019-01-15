---
title: MCDRemoteSystemAuthorizationKind
description:  Contains values that describe the potential authorization kinds (user-account-based authorization scopes)
for remote system discovery. 
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDRemoteSystemAuthorizationKind` 

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemAuthorizationKind)
```  

Contains values that describe the potential authorization kinds (user-account-based authorization scopes)
for remote system discovery. 

## Fields

| Name                              | Value | Description                    |
|:----------------------------------|:------|:-------------------------------|
| MCDRemoteSystemAuthorizationKindSameUser   | 0     | The system can only discover and connect with devices signed onto by the same user account.   |
| MCDRemoteSystemAuthorizationKindAnonymous | 1     | The system can discover and connect with other users' devices, provided they are in proximity and allow anonymous discovery.  |

