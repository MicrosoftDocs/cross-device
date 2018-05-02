---
title: RemoteSystemStatusTypeFilter
description: A class used to filter remote systems based on availability status type.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystemStatusTypeFilter class

```
public final class RemoteSystemStatusTypeFilter implements RemoteSystemFilter
```

A class used to filter remote systems based on availability status type.


## Constructors

### RemoteSystemStatusTypeFilter
`public RemoteSystemStatusTypeFilter(@NonNull RemoteSystemStatusType statusType)`

#### Parameters 
* `statusType` A value indicating the availability status type to filter for.

#### Returns
A new instance of this class with the given type filter.

## Methods

### getType
`RemoteSystemStatusType getType()`
Gets the remote system status type of this filter instance.

#### Returns
A [RemoteSystemStatusType](RemoteSystemStatusType.md) value indicating the type to filter for.


## Example

The following sample code initializes a RemoteSystemWatcher, adds filters to it, and starts the discovery process.

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