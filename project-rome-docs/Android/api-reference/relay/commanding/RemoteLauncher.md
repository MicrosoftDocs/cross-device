---
title: RemoteLauncher class
description: This class handles the launching of an app on a remote device through the use of a URI. 
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteLauncher class

```
public final class RemoteLauncher
```

This class handles the launching of an app on a remote device through the use of a URI.

## Constructors

### RemoteLauncher
`public RemoteLauncher()`

Creates an instance of this class.

## Methods

### launchUriAsync
`public AsyncOperation<RemoteLaunchUriStatus> launchUriAsync(
        @NonNull RemoteSystemConnectionRequest connectionRequest, @NonNull String uri)`

Starts the default app associated with the URI scheme name for the specified URI on a remote device.

#### Parameters  
* `connectionRequest` Specifies which remote system or application to connect to.
* `uri` The URI which will cause the launching of an app, according to its scheme.

### LaunchUriAsync
Starts the default app associated with the URI scheme name for the specified URI on a remote device, using the specified options.

`public AsyncOperation<RemoteLaunchUriStatus> launchUriAsync(
        @NonNull RemoteSystemConnectionRequest connectionRequest, @NonNull String uri, @NonNull RemoteLauncherOptions options)`

#### Parameters  
* `connectionRequest` Specifies which remote system or application to connect to.
* `uri` The URI which will cause the launching of an app, according to its scheme.
* `options` The launch specifications for the app.

## Example

The following sample code defines a method that uses a RemoteLauncher to launch a URI on a remote system or application.

```Java
/**
* Responsible for calling into the Rome API to launch the given URI and provides
* the logic to handle the RemoteLaunchUriStatus response.
* @param uri URI to launch
* @param system The RemoteSystemApplicationWrapper target for the launch URI request
*/
private void launchUri(final String uri, final RemoteSystemApplicationWrapper system, final long messageId)
{
        RemoteLauncher remoteLauncher = new RemoteLauncher();
        // note that the RemoteSystemApplicationWrapper "system"
        // can represent a RemoteSystem or RemoteSystemApplication.
        AsyncOperation<RemoteLaunchUriStatus> resultOperation = remoteLauncher.launchUriAsync(system.getRemoteSystemConnectionRequest(), uri);
        
        resultOperation.whenCompleteAsync(new AsyncOperation.ResultBiConsumer<RemoteLaunchUriStatus, Throwable>() {
                // Use a new AsyncOperation with an overridden method 
                // to handle the result of the launch attempt
                @Override
                public void accept(RemoteLaunchUriStatus status, Throwable throwable) throws Throwable {
                if (throwable != null) {
                        // handle a thrown exception
                        mLogList.logTraffic(String.format("Failed to launch uri [%s] because of exception [%s]", uri, throwable));
                } else {
                        if (status == RemoteLaunchUriStatus.SUCCESS) {
                                // handle success case
                                mLogList.logTraffic("Launch URI Success");
                        } else {
                                // handle a known error case
                                mLogList.logTraffic(String.format("Failed to launch uri [%s] because of exception [%s]", uri, status));
                        }
                }
                }
        });
}
```