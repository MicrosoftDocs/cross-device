---
title: MCDAppServiceRequest
description:  Represents an incoming message from a remote app/device to this app service connection.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDAppServiceRequest`

```
@interface MCDAppServiceRequest : NSObject
```
Represents an incoming message from a remote app/device to this app service connection.

## Properties

### message 
`@property(nonatomic, readonly, nonnull) NSDictionary* message;`

The message for the remote app service.

## Methods

### sendResponseAsync 
```
- (void)sendResponseAsync:(nonnull NSDictionary*)message
               completion:(nonnull void (^)(MCDAppServiceResponseStatus, NSError* _Nullable))completion;
```

Sends a response message to the remote app service that sent the request.

#### Parameters
* `message` 

The message for the remote app service.

#### Parameters
* `completion`     

The completion of the asynchronous operation with an MCDAppServiceResponseStatus value indicating the status of the send operation.