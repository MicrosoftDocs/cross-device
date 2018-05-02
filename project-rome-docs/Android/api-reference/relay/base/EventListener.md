---
title: EventListener
description: This interface provides a simple event handling method.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# EventListener interface

```
@FunctionalInterface public interface EventListener<TEventSource, TEventArg>
```

This interface provides a simple event handling method.

## Methods

### onEvent
`public void onEvent(TEventSource source, TEventArg arg);`

This method handles the event that was raised.

#### Parameters
* `source` The source object of the event.
* `arg` The event argument.

## Example
The following sample code shows a simple implementation of the EventListener interface. This class is meant to handle the "RemoteSystemAdded" event of the [RemoteSystemWatcher](../discovery/RemoteSystemWatcher.md) class, which marks the discovery of a remote system. 

```Java
// The following classes are used as event listeners for the watcher instance
private class RemoteSystemAddedListener implements EventListener<RemoteSystemWatcher, RemoteSystem> {
    @Override
    public void onEvent(RemoteSystemWatcher remoteSystemWatcher, RemoteSystem remoteSystem) {
        // add instance "remoteSystem" to program memory. See sample for full implementation.
    }
}
// ...
```