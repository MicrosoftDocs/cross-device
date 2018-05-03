---
title: NearShareFileProviderImpl 
description: This class is a sample implementation of the [NearShareFileProvider](NearShareFileProvider.md) interface. It is meant to be associated with one file.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# NearShareFileProviderImpl class

```
final class NearShareFileProviderImpl implements NearShareFileProvider
```

This class is a sample implementation of the [NearShareFileProvider](NearShareFileProvider.md) interface. It is meant to be associated with one file.

## Constructors

### NearShareFileProviderImpl
`public NearShareFileProviderImpl(Uri contentUri, Context context) throws IllegalArgumentException`

Creates a new instance of this class with an associated file.

#### Parameters
* `contentUri` A URI pointing to the file to be shared. The class will parse this file to deliver the necessary data.
* `context` The application context.

## Methods

### getFileName
`@Override
public String getFileName()`

Gets the name of the file to be shared.

#### Returns
The file name String.

### getSize
`@Override
public long getSize()`

Gets the size in bytes of the file to be shared.

#### Returns
The file size in bytes.

### open
`@Override
public NearShareStream open() throws IOException, NullPointerException`

This method creates a data stream for the file data.

#### Returns
A [NearShareStream](NearShareStream.md) instance representing the data.