---
title: NearShareFileProvider 
description: This interface contains methods that provide information about a file to be shared and create a [NearShareStream](NearShareStream.md) for this data.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareFileProvider interface

```
public interface NearShareFileProvider
```

This interface contains methods that provide information about a file to be shared and create a [NearShareStream](NearShareStream.md) for this data. [NearShareFileProviderImpl](NearShareFileProviderImpl.md) is a platform-provided implementation.

## Methods

### getFileName
`@NonNull public String getFileName();`

Gets the name of the file to be shared.

#### Returns
The file name String.

### getSize
`public long getSize();`

Gets the size in bytes of the file to be shared.

#### Returns
The file size in bytes.

### open
`@NonNull public NearShareStream open() throws IOException;`

This method creates a data stream for the file data.

#### Returns
A [NearShareStream](NearShareStream.md) instance representing the data.