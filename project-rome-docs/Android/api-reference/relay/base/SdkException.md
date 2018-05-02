---
title: SdkException
description: Exception used to communicate a failure from the Connected Devices Platform SDK.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# SdkException class

```
public final class SdkException extends RuntimeException
```

Exception used to communicate a failure from the Connected Devices Platform SDK. This is an unchecked exception that will be thrown for unexpected CDP-related errors.

## Methods

### getErrorCode
`public ErrorCode getErrorCode()`

#### Returns
The error code for this exception.