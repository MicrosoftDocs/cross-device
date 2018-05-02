---
title: AppServiceRequest 
description: Represents an incoming message from a remote app/device to this app service connection.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# AppServiceRequest class
```
public class AppServiceRequest
```

Represents an incoming message from a remote app/device to this app service connection.

## Methods

### getMessage
`public Map<String, Object> getMessage()`

Retrieves the message that was sent, consisting of key/value pairs.

#### Returns  
A [Map](https://developer.android.com/reference/java/util/Map.html) object containing String keys mapped to values of variable types.

### sendResponseAsync
`public AsyncOperation<AppServiceResponseStatus> sendResponseAsync(@Nullable Map<String, Object> response)`

Sends a response message to the remote app service that sent the request.

#### Parameters
* `response` A [Map](https://developer.android.com/reference/java/util/Map.html) object containing the data to be sent. 

#### Returns
An asynchronous operation with an [AppServiceResponseStatus](AppServiceResponseStatus.md) value indicating the status of the send operation.