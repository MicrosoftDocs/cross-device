---
title: RemoteSystemApplication
description: Represents an application on a remote system that is available for connectivity.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystemApplication class

```
public final class RemoteSystemApplication
```  

Represents an application on a remote system that is available for connectivity.

## Methods

### getId
`public String getId()`

Gets a unique identifier for this application.

#### Returns
A unique String identifier.

### getDisplayName
`public String getDisplayName()`

Gets the display-friendly name for this application.

#### Returns
A String of the display name.

### getIsAvailableByProximity
`public boolean getIsAvailableByProximity()`

Indicates whether this application is currently available for proximal connection.

#### Returns
true if the application is available for proximal connection, otherwise false.

### getIsAvailableBySpatialProximity
`public boolean getIsAvailableBySpatialProximity()`

Indicates whether this application is currently available for spatial sharing connection.

#### Returns
true if the application is available for spatial sharing, otherwise false.

### getAttributes
`public Map<String, String> getAttributes()`

Gets the attributes of this application.

#### Returns
A Map of key/value pairs defining the attributes.

## Example

The following sample code takes a previously-populated Map of discovered remote systems and creates a list of available systems *and* applications, using a wrapper class that can represent either.

``` Java
private ArrayMap<String, RemoteSystem> mSystems;

// ...

/**
* Returns a shallow copy of the current RemoteSystem ArrayMap.
* @return Shallow copy of the current RemoteSystem ArrayMap
*/
public ArrayList<RemoteSystemApplicationWrapper> getDiscoveredRemoteSystems() {
    ArrayList<RemoteSystemApplicationWrapper> result = new ArrayList<>();
    for (RemoteSystem system : mSystems.values()) {
        result.add(new RemoteSystemApplicationWrapper(system));
        for (RemoteSystemApplication application : system.getApplications()) {
            result.add(new RemoteSystemApplicationWrapper(application));
        }
    }
    return result;
}
```

The wrapper class from the sample is defined here:
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
