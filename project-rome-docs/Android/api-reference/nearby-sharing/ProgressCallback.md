---
title: ProgressCallback 
description: This class reports the progress of a file sharing operation. It is passed in as a parameter to a [NearShareSender](NearShareSender.md) method call and remains associated to that operation.
keywords: microsoft, windows, device relay, Android, Android api reference
---
# ProgressCallback class

```
public class ProgressCallback
```

This class reports the progress of a file sharing operation. It is passed in as a parameter to a [NearShareSender](NearShareSender.md) method call and remains associated to that operation.

## Constructors

### ProgressCallback
`public ProgressCallback()`

Creates a new instance of this class.

## Methods

### onProgress
`public void onProgress(NearShareProgress progress)`

This method is called by the platform when an increment of progress is made on a file sharing operation. The application can subscribe to this method and handle the data delivered in the parameter.

#### Parameters
* `progress` A [NearShareProgress](NearShareProgress.md) instance representing a snapshot of the current progress.