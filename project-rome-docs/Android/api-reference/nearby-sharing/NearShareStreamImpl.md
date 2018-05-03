---
title: NearShareStreamImpl 
description: This class is a sample implementation of the [NearShareStream](NearShareStream.md) interface. It is meant to represent a stream of data to be transferred through nearby sharing.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareStreamImpl class

```
final class NearShareStreamImpl implements NearShareStream 
```

This class is a sample implementation of the [NearShareStream](NearShareStream.md) interface. It is meant to represent a stream of data to be transferred through nearby sharing. Its methods are called by the platform during a share operation.

## Constructors

### NearShareStreamImpl
`public NearShareStreamImpl(Uri fileUri, Context context) throws Exception`

Creates a new instance of this class.

#### Parameters
* `fileUri` A URI pointing to the file to be shared.
* `context` The application context.

## Methods

### read
`public void read(long offset, int size, ByteBuffer byteBuffer);`

Reads the internal file data and writes it to the given [ByteBuffer](https://developer.android.com/reference/java/nio/ByteBuffer.html) reference.

#### Parameters
* `offset` The number of bytes to offset the starting point of the read operation by.
* `size` The size, in bytes, of the data.
* `byteBuffer` A [ByteBuffer](https://developer.android.com/reference/java/nio/ByteBuffer.html) instance into which the data will be written.
 

### close
`public void close() throws IOException;`

This method is called when the system is finished transferring files or the operation failed. It closes the internal file streams or channels that were open.