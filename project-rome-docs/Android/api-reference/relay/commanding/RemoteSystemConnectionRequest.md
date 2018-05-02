---
title: RemoteSystemConnectionRequest class
description: Represents an attempt to communicate with a specific remote device or application.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystemConnectionRequest class

```
public final class RemoteSystemConnectionRequest
```

Represents an attempt to communicate with a specific remote device or application.

## Constructors

### RemoteSystemConnectionRequest
`public RemoteSystemConnectionRequest(@NonNull RemoteSystem remoteSystem)`

Initializes a new instance of the RemoteSystemConnectionRequest class for a particular remote system. This constructor is not recommended, as it does not specify an app to target and therefore may result in an unexpected app being selected to service requests sent to the system.

#### Parameters  
* `remote` The RemoteSystem object to attempt to connect to.

### RemoteSystemConnectionRequest
`public RemoteSystemConnectionRequest(@NonNull RemoteSystemApplication remoteSystemApplication)`

Initializes a new instance of the RemoteSystemConnectionRequest class for a particular application on a remote system.

#### Parameters
* `remoteSystemApplication` The remote application to attempt to connect to.

## Public methods

### getRemoteSystem
Retrieves the RemoteSystem object for this particular connection request.

`public RemoteSystem getRemoteSystem()`

#### Returns  
The RemoteSystem object for this particular connection request

## Example

The following sample class is a wrapper for [RemoteSystem](../discovery/RemoteSystem.md) and [RemoteSystemApplication](../discovery/RemoteSystemApplication.md) instances. It contains the functionality for creating a RemoteSystemConnectionRequest.

```Java
import android.content.Context;

import com.microsoft.connecteddevices.commanding.RemoteSystemConnectionRequest;
import com.microsoft.connecteddevices.discovery.RemoteSystem;
import com.microsoft.connecteddevices.discovery.RemoteSystemApplication;

/**
 * This class abstracts the type (either a Remote System or Application) and allows both objects to
 * be used as the same object.
 */
public class RemoteSystemApplicationWrapper {
    // Member Variables
    // These objects are mutually exclusive, the wrapper can only be constructed with 1 type
    private RemoteSystem mRemoteSystem = null;
    private RemoteSystemApplication mRemoteSystemApplication = null;

    // Constructors
    public RemoteSystemApplicationWrapper(RemoteSystemApplication remoteSystemApplication) {
        this.mRemoteSystemApplication = remoteSystemApplication;
    }

    public RemoteSystemApplicationWrapper(RemoteSystem remoteSystem) {
        this.mRemoteSystem = remoteSystem;
    }

    /**
     * Returns a string containing the type (either system or application) with the name of the object.
     * @return String containing the type (either system or application) with the name of the object.
     */
    public String getDisplayName() {
        if (mRemoteSystem != null) {
            return "[System] " + mRemoteSystem.getDisplayName();
        }
        return "[App] " + mRemoteSystemApplication.getDisplayName();
    }

    // returns string that will show the whether or not the system or application is available (uses resource strings defined elsewhere)
    public String getAvailabilityStatus(Context context) {
        if (mRemoteSystem != null) {
            return "Status: " + mRemoteSystem.getStatus().toString();
        }
        String proximity = context.getString((mRemoteSystemApplication
                .getIsAvailableByProximity()) ?
                R.string.available_text : R.string.unavailable_text);
        String spatial = context.getString((mRemoteSystemApplication
                .getIsAvailableBySpatialProximity()) ?
                R.string.available_text : R.string.unavailable_text);
        return String.format("Proximity: %s, Spatial: %s", proximity, spatial);
    }

    /**
     * Creates and returns a new RemoteSystemConnectionRequest containing the stored system or app.
     * @return
     */
    public RemoteSystemConnectionRequest getRemoteSystemConnectionRequest() {
        if (mRemoteSystem != null) {
            return new RemoteSystemConnectionRequest(mRemoteSystem);
        }
        return new RemoteSystemConnectionRequest(mRemoteSystemApplication);
    }
}
