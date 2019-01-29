---
title: MCDAppServiceResponse
description:  A class that represents a response received from a connected remote app service.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDAppServiceResponse`

```
@interface MCDAppServiceResponse : NSObject
```

A class that represents a response received from a connected remote app service.

## Properties

### message 
`@property(nonatomic, readonly, nonnull) NSDictionary* message;`

The message received from the remote app service.

### status
`@property(nonatomic, readonly) MCDAppServiceResponseStatus status;`

The status of the response received.