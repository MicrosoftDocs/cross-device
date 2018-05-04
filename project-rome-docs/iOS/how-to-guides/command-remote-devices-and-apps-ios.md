---
title: Command remote devices and apps (iOS)
description: This guide will show how to discover remote devices and apps and then launch apps or interact with app services.
keywords: microsoft, windows, project rome, iOS api reference 
---


# Command remote devices and apps (iOS)

> **Important:** Before you use this guide, make sure you have completed all of the preliminary steps laid out in [Getting started with Connected Devices](getting-started-rome-iOS.md).

The commanding scenarios, featured in the Device Relay namespaces, use a watcher pattern in which available devices are detected over time through various types of network connections and corresponding events are raised. This guide will show how to discover remote devices and apps and then launch apps or interact with app services.

## Discover remote devices and apps

A **MCDRemoteSystemWatcher** instance will handle the core functionality of this section.

```ObjectiveC
// Create a RemoteSystemWatcher to discover devices
MCDRemoteSystemWatcher* _watcher;
```

Before you create a watcher and start discovering devices, you may wish to add discovery filters to determine which kinds of devices your app will target. These can be determined by the user or hard-coded into the app, depending on your use case.

The following code from the sample demonstrates the creation and starting of the watcher instance. Note that event handlers are registered just before; these will allow your app to parse and interact with the devices that are discovered. 

```ObjectiveC
// Start watcher with filter for transport types, form factors
- (void)startWatcherWithFilter:(NSMutableArray<NSObject<MCDRemoteSystemFilter>*>*)remoteSystemFilter
{
    _discoveredSystems = [[NSMutableArray alloc] init];
    _devicesAdded = 0;
    _devicesUpdated = 0;
    _devicesRemoved = 0;

    _watcher = (remoteSystemFilter.count > 0) ? [[MCDRemoteSystemWatcher alloc] initWithFilters:remoteSystemFilter] :
        [[MCDRemoteSystemWatcher alloc] init];

    RemoteSystemViewController* __weak weakSelf = self;
    [_watcher addRemoteSystemAddedListener:^(
        __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemAdded:system]; }];

    [_watcher addRemoteSystemUpdatedListener:^(
        __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemUpdated:system]; }];

    [_watcher addRemoteSystemRemovedListener:^(
        __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemRemoved:system]; }];
    [_watcher start];
}
```

The event handler methods are defined here.

```ObjectiveC
// Handle when RemoteSystems are added
- (void)_onRemoteSystemAdded:(MCDRemoteSystem*)system
{
    @synchronized(self)
    {
        _devicesAdded++;
        [_discoveredSystems addObject:system];
        [_delegate remoteSystemsDidUpdate];
    }
}

// Handle when RemoteSystems are updated
- (void)_onRemoteSystemUpdated:(MCDRemoteSystem*)system
{
    @synchronized(self)
    {
        _devicesUpdated++;

        for (unsigned i = 0; i < _discoveredSystems.count; i++)
        {
            MCDRemoteSystem* cachedSystem = [_discoveredSystems objectAtIndex:i];
            if ([cachedSystem.displayName isEqualToString:system.displayName])
            {
                [_discoveredSystems replaceObjectAtIndex:i withObject:system];
                break;
            }
        }
    }
}

// Handle when RemoteSystems are removed
- (void)_onRemoteSystemRemoved:(MCDRemoteSystem*)system
{
    @synchronized(self)
    {
        _devicesRemoved++;

        for (unsigned i = 0; i < _discoveredSystems.count; i++)
        {
            MCDRemoteSystem* cachedSystem = [_discoveredSystems objectAtIndex:i];
            if ([cachedSystem.displayName isEqualToString:system.displayName])
            {
                [_discoveredSystems removeObjectAtIndex:i];
                break;
            }
        }
    }
}
```

It is recommended that your app maintain a list of discovered devices (represented by **MCDRemoteSystem** instances) and display information about available devices and their apps (such as display name and device type) on the UI. 

Once `[_watcher start]` is called, it will begin watching for remote system activity and will raise events when connected devices are discovered, updated, or removed from the set of detected devices. It will scan continuously in the background, so it is recommended that you stop the watcher (with `[_watcher stop]`) when you no longer need it to avoid unnecessary network communication and battery drain.

At this point in your code, you should have a working list of **MCDRemoteSystem** objects that refer to available devices. What you do with these devices will depend on the function of your app. The three major types of actions are remote launching, remote app services, and nearby file sharing. They are explained in the following three sections.

## A) Remote launching

The following code shows how to select one of these objects (ideally this is done through a UI control) and then use **MCDRemoteLauncher** to launch an app on it by passing an app-compatible URI. 

It's important to note that a remote launch can target a remote device (in which case the host device will launch the given URI with its default app for that URI scheme) _or_ a specific remote application on that device. 

Depending on the URI that is sent, you can launch an app in a specific state or configuration on a remote device. This allows for the ability to continue a user task, like watching a movie, on a different device without interruption. 

As the previous section demonstrates, discovery happens at the device level first (a **MCDRemoteSystem** represents a device), but you can call the `getApplications` method on a **MCDRemoteSystem** instance to get an array of **MCDRemoteSystemApplication** objects, which represent apps on the remote device that have been registered to use the Connected Devices Platform (just as you registered your own app in the [Getting started guide](getting-started-rome-iOS)). Both **MCDRemoteSystem** and **MCDRemoteSystemApplication** can be used to construct a **MCDRemoteSystemConnectionRequest**, which is what is needed to launch a URI.

The following code from the sample shows the remote launching of a URI over a connection request.

```ObjectiveC
// Send a remote launch of a uri to RemoteSystemApplication
- (IBAction)launchUriButton:(id)sender
{
    NSString* uri = self.uriField.text;
    MCDRemoteLauncher* remoteLauncher = [[MCDRemoteLauncher alloc] init];
    MCDRemoteSystemConnectionRequest* connectionRequest =
        [MCDRemoteSystemConnectionRequest requestWithRemoteSystemApplication:self.selectedApplication];
    [remoteLauncher launchUriAsync:uri
        withConnectionRequest:connectionRequest
            completion:^(MCDRemoteLaunchUriStatus result, NSError* _Nullable error) {
                if (error)
                {
                    NSLog(@"LaunchURI [%@]: ERROR: %@", uri, error);
                    return;
                }

                if (result == MCDRemoteLaunchUriStatusSuccess)
                {
                    NSLog(@"LaunchURI [%@]: Success!", uri);
                }
                else
                {
                    NSLog(@"LaunchURI [%@]: Failed with code %d", uri, (int)result);
                }
            }];
}
```


Depending on your use, you may need to cover the cases in which no apps on the targeted system can handle the URI, or multiple apps can handle it. The **[MCDRemoteLauncher](../api-reference/relay/discovery/MCDRemoteLauncher.md)** class and **[MCDRemoteLauncherOptions](../api-reference/relay/discovery/MCDRemoteLauncherOptions.md)** class describe how to do this.

## B) Remote app services

Your iOS app can use the Connected Devices Portal interact with app services on other devices.

This provides many ways to communicate with other devices&mdash;all without needing to bring an app to the foreground of the host device. 

### Set up the app service on the target device
You will need a remote app service to target. For a simple test, you can use the [Roman Test App for Windows](http://aka.ms/romeapp) as your target app service; download the app a Windows device and make sure you are signed in with the same MSA account you used in the [Getting started guide](getting-started-rome-iOS.md). 

For instructions on how to write your own UWP app service, see [Create and consume an app service](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service).

If you are writing your own app service on Windows, you will need to make a few edits in order to make the service compatible with Connected Devices. In Visual Studio, go to the app service provider project and select its _Package.appxmanifest_ file. Right-click and select **View Code** to view the full contents of the file. Find the **Extension** element that defines the project as an app service and names its parent project.

``` xml
...
<Extensions>
    <uap:Extension Category="windows.appService" EntryPoint="RandomNumberService.RandomNumberGeneratorTask">
        <uap:AppService Name="com.microsoft.randomnumbergenerator"/>
    </uap:Extension>
</Extensions>
...
```

Change the namespace of the **AppService** element to **uap3** and add the **SupportsRemoteSystems** attribute:

``` xml
...
<uap3:AppService Name="com.microsoft.randomnumbergenerator" SupportsRemoteSystems="true"/>
...
```

In order to use elements in this new namespace, you must add the namespace definition at the top of the manifest file.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<Package
  xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
  xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
  xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
  xmlns:uap3="http://schemas.microsoft.com/appx/manifest/uap/windows10/3">
  ...
</Package>
```

Build your app service provider project and deploy it to the target device(s).

### Open an app service connection on the client device
Your iOS app must acquire a reference to a remote device or application. Like the launch section, this scenario requires the use of a **MCDRemoteSystemConnectionRequest**, which can be constructed from either a **MCDRemoteSystem** or a **MCDRemoteSystemApplication** representing an available app on the system.

Additionally, your app will need to identify its targeted app service by two strings: the *app service name* and *package identifier*. These are found in the source code of the app service provider (see [Create and consume an app service](https://msdn.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service) for details). Together they construct the **MCDAppServiceDescription**, which is fed into an **MCDAppServiceConnection**.

So, an **MCDAppServiceConnection** uses a **MCDRemoteSystemConnectionRequest** to determine which remote system or app to target, and it uses its internal **MCDAppServiceDescription** to determine the app service. This is necessary because a single app could provide multiple app services.

```ObjectiveC
// Step #1:  Establish an app service connection
- (IBAction)connectAppServiceButton:(id)sender
{
    MCDAppServiceConnection* connection = nil;
    @synchronized(self)
    {
        connection = _appServiceConnection;
        if (!connection)
        {
            connection = _appServiceConnection = [MCDAppServiceConnection new];
            connection.appServiceDescription =
                [MCDAppServiceDescription descriptionWithName:g_appServiceName packageId:g_packageIdentifier];
            _serviceClosedRegistration = [connection addServiceClosedListener:^(__unused MCDAppServiceConnection* connection,
                MCDAppServiceClosedStatus status) { [self appServiceConnection:connection closedWithStatus:status]; }];
        }
    }

    @try
    {
        MCDRemoteSystemConnectionRequest* connectionRequest =
            [MCDRemoteSystemConnectionRequest requestWithRemoteSystemApplication:self.selectedApplication];
        [connection openRemoteAsync:connectionRequest
            completion:^(MCDAppServiceConnectionStatus status, NSError* error) {
                if (error)
                {
                    NSLog(@"ConnectAppService: ERROR: %@", error);
                    return;
                }
                if (status != MCDAppServiceConnectionStatusSuccess)
                {
                    NSLog(@"ConnectAppService: Failed with code %d", (int)status);
                    return;
                }
                NSLog(@"Successfully connected!");
                dispatch_async(
                    dispatch_get_main_queue(), ^{ self.appServiceStatusLabel.text = @"App service connected! no ping sent"; });
            }];
    }
    @catch (NSException* ex)
    {
        NSLog(@"ConnectAppService: EXCEPTION! %@", ex);
    }
}
```


### Create a message to send to the app service

On iOS, the messages that you send to remote app services will be of the **NSDictionary** type.

> Note: When your app communicates with app services on other platforms, the Connected Devices Platform translates the **NSDictionary** into the equivalent construct on the receiving platform. For example, a **[NSDictionary](https://developer.apple.com/documentation/foundation/nsdictionary)** sent from this app to a Windows app service gets translated into a [**ValueSet**](https://msdn.microsoft.com/library/windows/apps/windows.foundation.collections.valueset) object (of the .NET Framework), which can then be interpreted by the app service. Information passed in the other direction undergoes the reverse translation.

The following method crafts a message that can be interpreted by the Roman Test App's app service for Windows.

```ObjectiveC
// Create a message to send
- (NSDictionary*)_createPingMessage
{
    return @{
        @"Type" : @"ping",
        @"CreationDate" : [_dateFormatter stringFromDate:[NSDate date]],
        @"TargetId" : _selectedApplication.applicationId
    };
}
```

### Send messages to the app service

Once the app service connection is established and the message is created, sending it to the app service is simple and can be done from anywhere in the app that has a reference to the connection instance and the message.

The following code from the sample shows the sending of a message to an app service and the handling of the response.

```ObjectiveC
//  Send a message using the app service connection
- (IBAction)sendAppServiceButton:(id)sender
{
    if (!_appServiceConnection)
    {
        return;
    }

    // Send the message and get a response
    @try
    {
        [_appServiceConnection sendMessageAsync:[self _createPingMessage]
            completion:^(MCDAppServiceResponse* response, NSError* error) {
                if (error)
                {
                    NSLog(@"SendPing: ERROR: %@", error);
                    return;
                }

                if (response.status != MCDAppServiceResponseStatusSuccess)
                {
                    NSLog(@"SendPing: Response received with bad status code %d", (int)response.status);
                    return;
                }

                NSString* creationDateString = response.message[@"CreationDate"];
                if (creationDateString)
                {
                    NSDate* date = [_dateFormatter dateFromString:creationDateString];
                    if (date)
                    {
                        NSTimeInterval diff = [[NSDate date] timeIntervalSinceDate:date];
                        dispatch_async(dispatch_get_main_queue(),
                            ^{ self.appServiceStatusLabel.text = [NSString stringWithFormat:@"%g", diff]; });
                    }
                }
            }];
    }
    @catch (NSException* ex)
    {
        NSLog(@"SendPing: EXCEPTION! %@", ex);
    }
}
```
In the Roman App case, the response contains the date it was created, so in this very simple use case, we can compare the dates to get the total transit time of the message response.

That concludes a single message exchange with a remote app service.

### Finish app service communication

When your app is finished interacting with the target device's app service, close the connection between the two devices.

```ObjectiveC
- (void)appServiceConnection:(__unused MCDAppServiceConnection*)connection closedWithStatus:(MCDAppServiceClosedStatus)status
{
    NSLog(@"AppService closed with status %d", (int)status);
    dispatch_async(
        dispatch_get_main_queue(), ^{ self.appServiceStatusLabel.text = [NSString stringWithFormat:@"disconnected (%d)", (int)status]; });
}
```

## Related topics
* [Getting started with Connected Devices (iOS)](getting-started-rome-iOS.md)
* [Create and consume an app service](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service).
