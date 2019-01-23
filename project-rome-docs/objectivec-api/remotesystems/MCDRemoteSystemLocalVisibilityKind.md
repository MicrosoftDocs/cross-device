---
title: MCDRemoteSystemLocalVisibilityKind
description:  Contains values that describe the local application visibility preference when discovering remote systems.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# enum `MCDRemoteSystemLocalVisibilityKind` 

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemLocalVisibilityKind)
```  
Contains values that describe the local application visibility preference when discovering remote
systems.

## Fields

| Name                              | Value | Description                    |
|:----------------------------------|:------|:-------------------------------|
| MCDRemoteSystemLocalVisibilityKindShowAll | 0 | Show all discoverable applications, including the calling app.
| MCDRemoteSystemLocalVisibilityKindHideLocalApp | 1 | Hide the calling application.