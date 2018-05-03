---
title: NearShareStream 
description: This interface contains methods for reading file data to be transferred through nearby sharing. It is used by the platform during a share operation.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareStream interface

```
public interface NearShareStream extends AutoCloseable
```

This interface contains methods for reading file data to be transferred through nearby sharing. It is used by the platform during a share operation. [NearShareStreamImpl](NearShareStreamImpl.md) is a platform-provided implementation.

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

This method is called when the system is finished transferring files or the operation failed. It should close any internal file streams or channels that were open.