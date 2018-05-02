---
title: RemoteSystem
description: A class to represent a remote system.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystem class

```
public final class RemoteSystem
```  

A class to represent a remote system.

## Methods

### getKind
`public String getKind()`

Gets the device type of this remote system.

#### Returns
A String of the canonical name of the device type.

### getId
`public String getId()`

Gets the identifier for this remote system.

#### Returns
A unique ID String.

### getDisplayName
`public String getDisplayName()`

Gets the friendly display name of this remote system.

#### Returns
A String of the display-friendly name.

### getStatus
`public RemoteSystemStatus getStatus() `

Gets the availability status of the remote system.

#### Returns
A [RemoteSystemStatus](RemoteSystemStatus.md) value describing the status.

### getManufacturerDisplayName
`public String getManufacturerDisplayName()`

Gets the display name of the remote system manufacturer.

#### Returns
A String of the manufacturer name.

### getModelDisplayName
`public String getModelDisplayName()`

Gets the display name of the remote system model.

#### Returns 
A String of the model name.

### getApplications
`public RemoteSystemApplication[] getApplications()`

Gets an array of the applications on this remote system that are available for connectivity.

#### Returns
An array of [RemoteSystemApplication](RemoteSystemApplication.md) instances.

### getPlatform
`RemoteSystemPlatform getPlatform()`

Gets the RemoteSystemPlatform managing remote system activity.

#### Returns
The [RemoteSystemPlatform](RemoteSystemPlatform.md) instance.

## Example

The following sample code initializes a [RemoteSystemWatcher](RemoteSystemWatcher.md), adds filters to it, and starts the discovery process. Event listeners handle new RemoteSystem instances as they are discovered.

```Java

// This method creates, initializes, and starts a RemoteSystemWatcher.
private void onStartWatcherClicked() {
    //RemoteSystemWatcher cannot be started unless the platform is initialized and the user is logged in
    if (!getMainActivity().isSignedIn()) {
        return;
    }
    if (!getMainActivity().isPlatformInitialized()) {
        return;
    }

    // create a list of filters. Filter choices below are arbitrary. Ideally, the app extracts desired filter configuration from the UI.
    ArrayList<RemoteSystemFilter> filters = new ArrayList<>();

    /*  RemoteSystemDiscoveryType filters can be used to filter the types of Remote Systems we discover
    Possible values:
        ANY(0),
        PROXIMAL(1),
        CLOUD(2),
        SPATIALLY_PROXIMAL(3)
    */
        filters.add(new RemoteSystemDiscoveryTypeFilter(RemoteSystemDiscoveryType.ANY));

    /*  RemoteSystemStatusType filters can be used to filter the status of Remote Systems we discover
        Possible values:
            ANY(0),
            AVAILABLE(1)
    */
    filters.add(new RemoteSystemStatusTypeFilter(RemoteSystemStatusType.AVAILABLE));
    

    /*  RemoteSystemKindFilter can filter the types of devices you want to discover
        // Possible values are members of the RemoteSystemKinds class.
        */
    String[] kinds = new String[] { RemoteSystemKinds.Phone(), RemoteSystemKinds.Tablet() };

    RemoteSystemKindFilter kindFilter = new RemoteSystemKindFilter(kinds);
    filters.add(kindFilter);
    

    /*  RemoteSystemAuthorizationKind determines the types of user you want to discover
        Possible values:
            SAME_USER(0),
            ANONYMOUS(1)
    */

    filters.add(new RemoteSystemAuthorizationKindFilter(RemoteSystemAuthorizationKind.SAME_USER));


    if (filters.isEmpty()) {
        mWatcher = new RemoteSystemWatcher();
    } else {
        mWatcher = new RemoteSystemWatcher(filters.toArray(new RemoteSystemFilter[filters.size()]));
    }

    //Use these events to keep the list of Remote Systems up to date (class definitions below)
    mWatcher.addRemoteSystemAddedListener(new RemoteSystemAddedListener());
    mWatcher.addRemoteSystemUpdatedListener(new RemoteSystemUpdatedListener());
    mWatcher.addRemoteSystemRemovedListener(new RemoteSystemRemovedListener());
    mWatcher.addErrorOccurredListener(new RemoteSystemWatcherErrorOccurredListener());

    clearSystems();

    try {
        mWatcher.start();
        mStartedRemoteSystemWatcher = true;
    } catch (Exception e) { WriteApiException("RemoteSystemWatcher.start", e); }
}

// The following classes are used as event listeners for the watcher instance
private class RemoteSystemAddedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // add instance "remoteSystem" to program memory. See sample for full implementation.
    }
}

private class RemoteSystemUpdatedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // update instance "remoteSystem" in program memory. See sample for full implementation.
    }
}

private class RemoteSystemRemovedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // remove instance "remoteSystem" from program memory. See sample for full implementation.
    }
}

private class RemoteSystemWatcherErrorOccurredListener implements EventListener<RemoteSystemWatcher, RemoteSystemWatcherError> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystemWatcherError remoteSystemWatcherError) {
        // handle error
    }
}
```