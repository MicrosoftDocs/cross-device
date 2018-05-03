---
title: NearShareSender 
description: This class is responsible for sending URIs and/or files from one device to another through the nearby sharing feature.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareSender class

```
public final class NearShareSender
```

This class is responsible for sending URIs and/or files from one device to another through the nearby sharing feature.

## Constructors

### NearShareSender
`public NearShareSender()`

Creates a new instance of this class.

## Methods

### sendUriAsync
`@NonNull
public AsyncOperation<NearShareStatus> sendUriAsync(RemoteSystemConnectionRequest remoteSystemConnectionRequest, String uri)`

Sends a single URI to a remote device or app.

#### Parameters
* `remoteSystemConnectionRequest` A [RemoteSystemConnectionRequest](../relay/commanding/RemoteSystemConnectionRequest.md) indicating the device or app to connect to.
* `uri` The URI string to send.

#### Returns
An asynchronous operation with a [NearShareStatus](NearShareStatus.md) value.

### sendFilesAsync
`@NonNull
public AsyncOperation<NearShareStatus> sendFilesAsync(RemoteSystemConnectionRequest remoteSystemConnectionRequest, NearShareFileProvider[] files, ProgressCallback progressCallback)`

Sends multiple files to a remote device or app.

#### Parameters
* `remoteSystemConnectionRequest` A [RemoteSystemConnectionRequest](../relay/commanding/RemoteSystemConnectionRequest.md) indicating the device or app to connect to.
* `files` A [NearShareFileProvider](NearShareFileProvider.md) array representing the list of files to send.
* `progressCallback` A [ProgressCallback](ProgressCallback.md) instance to be associated with this operation. It can be queried to report on the status of the operation.

#### Returns
An asynchronous operation with a [NearShareStatus](NearShareStatus.md) value.

### sendFileAsync
`@NonNull 
public AsyncOperation<NearShareStatus> sendFileAsync(RemoteSystemConnectionRequest remoteSystemConnectionRequest, NearShareFileProvider file, ProgressCallback progressCallback)`

Sends a single file to a remote device or app.

#### Parameters
* `remoteSystemConnectionRequest` A [RemoteSystemConnectionRequest](../relay/commanding/RemoteSystemConnectionRequest.md) indicating the device or app to connect to.
* `file` A [NearShareFileProvider](NearShareFileProvider.md) instance representing the file to send.
* `progressCallback` A [ProgressCallback](ProgressCallback.md) instance to be associated with this operation. It can be queried to report on the status of the operation.

#### Returns
An asynchronous operation with a [NearShareStatus](NearShareStatus.md) value.

### isNearShareSupported
`public boolean isNearShareSupported(RemoteSystemConnectionRequest remoteSystemConnectionRequest)`

Reports whether all conditions are satisfied for the app to share with a remote device or app (for example, if the device is signed in with a different user account, then both devices must have their nearby sharing settings set to "everyone").

#### Parameters
* `remoteSystemConnectionRequest` A [RemoteSystemConnectionRequest](../relay/commanding/RemoteSystemConnectionRequest.md) indicating the device or app that this app is intending to share with.

#### Returns
**true** if the conditions are met to initiate nearby sharing, **false** if not.