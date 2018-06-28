---
title: RemoteSystemWatcher
description: A class used to discover remote systems.
keywords: microsoft, windows, device relay, Android, Android api reference
---

# RemoteSystemWatcher class

```
public final class RemoteSystemWatcher
```

A class used to discover remote systems.

## Constructors

### RemoteSystemWatcher
`public RemoteSystemWatcher(@NonNull RemoteSystemFilter[] filters) `

Creates and initializes a new instance of this class.

#### Parameters
* `filters` [optional] An array of [RemoteSystemFilter](RemoteSystemFilter.md) instances to use in the device discovery process.

## Methods

### start
`public void start()`

Begins discovering remote systems.

### stop
`public void stop()` 

Stops the active discovery.

### addRemoteSystemAddedListener
`public long addRemoteSystemAddedListener(@NonNull EventListener<RemoteSystemWatcher, RemoteSystem> listener)`

Adds a listener for the "remote system added" event.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeRemoteSystemAddedListener
`public void removeRemoteSystemAddedListener(long eventRegistrationToken)`

Removes a listener from the "remote system added" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addRemoteSystemUpdatedListener
`public long addRemoteSystemUpdatedListener(@NonNull EventListener<RemoteSystemWatcher, RemoteSystem> listener)`

Adds a listener for the "remote system updated" event.

>**Note:** This event is raised when a remote system (device) that was previously discovered in this discovery session changes from proximally connected to cloud connected, or the reverse. It is also raised when a remote system changes one of its monitored properties (see the properties of the **RemoteSystem** class).

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeRemoteSystemUpdatedListener
`public void removeRemoteSystemUpdatedListener(long eventRegistrationToken) `

Removes a listener from the "remote system updated" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addRemoteSystemRemovedListener
`public long addRemoteSystemRemovedListener(@NonNull EventListener<RemoteSystemWatcher, RemoteSystem> listener)`

Adds a listener for the "remote system removed" event.

> **Note:** The "remote system removed" event is raised only after a RemoteSystem has stopped being discoverable over all of the categories specified by the associated **RemoteSystemDiscoveryTypeFilter**.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeRemoteSystemRemovedListener
`public void removeRemoteSystemRemovedListener(long eventRegistrationToken)`

Removes a listener from the "remote system removed" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addEnumerationCompletedListener 
`public long addEnumerationCompletedListener(@NonNull EventListener<RemoteSystemWatcher, Void> listener)`

Adds a listener for the "enumeration completed" event.

> The "enumeration completed" event is raised for different criteria depending on the discovery type(s), but in every case it is meant to signify the time when all available devices can be expected to have been discovered.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeEnumerationCompletedListener
`public void removeEnumerationCompletedListener(long eventRegistrationToken)`

Removes a listener from the "enumeration completed" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

### addErrorOccurredListener
`public long addErrorOccurredListener(@NonNull EventListener<RemoteSystemWatcher, RemoteSystemWatcherError> listener)`

Adds a listener for the "error occurred" event.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration ID.

### removeErrorOccurredListener
`public void removeErrorOccurredListener(long eventRegistrationToken)`

Removes a listener from the "error occurred" event.

#### Parameters 
* `eventRegistrationToken` The ID of the event registration to remove.

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