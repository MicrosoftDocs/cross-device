---
title: MCDStatelessAppServiceResponse
description:  Represents a message passed from a remote app service to the client app in response to a
previous call to MCDAppServiceConnection.sendStatelessMessageAsync.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDStatelessAppServiceResponse` 

```
@interface MCDStatelessAppServiceResponse : NSObject
```  

Represents a message passed from a remote app service to the client app in response to a
previous call to MCDAppServiceConnection.sendStatelessMessageAsync.


## Properties

### message
`@property(nonatomic, readonly, nonnull) NSDictionary* message;`

The message sent by the remote app service, consisting of key/value pairs.

### status
`@property(nonatomic, readonly) MCDStatelessAppServiceResponseStatus status;`

The status of the response from the remote app service.

