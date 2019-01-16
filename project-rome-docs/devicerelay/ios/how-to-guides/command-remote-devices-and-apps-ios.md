---
title: Command remote devices and apps (iOS)
description: This guide will show how to discover remote devices and apps and then launch apps or interact with app services.
ms.date: 07/17/2018
ms.topic: article
keywords: microsoft, windows, project rome, commanding, ios
ms.assetid: b5d426db-a0ca-4888-b2cb-cb7fdb1c6c0d
ms.localizationpriority: medium
---

# Command remote devices and apps (iOS)

Here you will find guidance on how to implement commanding scenarios in your iOS apps.  

See the [API reference](../api-reference/index.md) page for links to the reference docs relevant to these scenarios. This guide is intended to provide the necessary steps to onboard with the Connected Devices Platform, the underlying platform of the Project Rome features.  See the [iOS sample app](https://github.com/Microsoft/project-rome/tree/master/iOS/samples) for a working example of these features.  

[!INCLUDE [ios/preliminary-setup](../../../includes/ios/preliminary-setup.md)]

The commanding scenarios, featured in the Device Relay namespaces, use a watcher pattern in which available devices are detected over time through various types of network connections and corresponding events are raised. This guide will show how to discover remote devices and apps and then launch apps or interact with app services.  Depending on the scenario, there is an additional step required to command an iOS device.  For sending commands *to* iOS the platform requires that you onboard your app with the Microsoft Windows Dev Center so notification can be sent to the device.  If this is not a scenario requirement, simply skip the 'Register your app in Microsoft Windows Dev Center for cross-device experiences' as this is not needed.

[!INCLUDE [ios/notifications-dev-center-onboarding](../../../includes/ios/notifications-dev-center-onboarding.md)]

Now you are ready to start working with the platform.  It is important to follow the steps identified below to ensure a seamless onboarding experience.

[!INCLUDE [ios/create-setup-events-start-platform](../../../includes/ios/create-setup-events-start-platform.md)]

Now, you're ready to start using RemoteSystems.

[!INCLUDE [ios/remote-system-registration](../../../includes/ios/remote-system-registration.md)]

## Discover remote devices and apps

An **MCDRemoteSystemWatcher** instance will handle the core functionality of this section. Declare it in the class which is to discover remote systems.

```ObjectiveC
// Create a RemoteSystemWatcher to discover devices
MCDRemoteSystemWatcher* _watcher;
```

Before you create a watcher and start discovering devices, you may wish to add discovery filters to determine which kinds of devices your app will target. These can be determined by user input or hard-coded into the app, depending on your use case.

The following code from the sample app demonstrates the creation and starting of the watcher instance. Note that event handlers are registered just before; these will allow your app to parse and interact with the devices that are discovered. 

```ObjectiveC
// Start watcher with filter for transport types, form factors
- (void)startWatcherWithFilter:(NSMutableArray<NSObject<MCDRemoteSystemFilter>*>*)remoteSystemFilter
{
    _discoveredSystems = [[NSMutableArray alloc] init];
    _devicesAdded = 0;
    _devicesUpdated = 0;
    _devicesRemoved = 0;

    // add filters (not defined here)
    _watcher = (remoteSystemFilter.count > 0) ? [[MCDRemoteSystemWatcher alloc] initWithFilters:remoteSystemFilter] :
        [[MCDRemoteSystemWatcher alloc] init];

    // add event handlers
    RemoteSystemViewController* __weak weakSelf = self;
    [_watcher addRemoteSystemAddedListener:^(
        __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemAdded:system]; }];

    [_watcher addRemoteSystemUpdatedListener:^(
        __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemUpdated:system]; }];

    [_watcher addRemoteSystemRemovedListener:^(
        __unused MCDRemoteSystemWatcher* watcher, MCDRemoteSystem* system) { [weakSelf _onRemoteSystemRemoved:system]; }];
    
    // start watcher
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

We recommend that your app maintain a set of discovered devices (represented by **MCDRemoteSystem** instances) and display information about available devices and their apps (such as display name and device type) on the UI. 

Once `[_watcher start]` is called, it will begin watching for remote system activity and will raise events when connected devices are discovered, updated, or removed from the set of detected devices. It will scan continuously in the background, so it is recommended that you stop the watcher (with `[_watcher stop]`) when you no longer need it to avoid unnecessary network communication and battery drain.

## Implement a commanding scenario
At this point in your code, you should have a working list of **MCDRemoteSystem** objects that refer to available devices. What you do with these devices will depend on the function of your app. The main types of interaction are remote launching and remote app services. They are explained in the following sections.

### A) Remote launching

The following code shows how to select one of these objects (ideally this is done through a UI control) and then use **MCDRemoteLauncher** to launch an app on it by passing an app-compatible URI. 

It's important to note that a remote launch can target a remote device (in which case the host device will launch the given URI with its default app for that URI scheme) _or_ a specific remote application on that device. 


As the previous section demonstrated, discovery happens at the device level first (an **MCDRemoteSystem** represents a device), but you can call the `getApplications` method on an **MCDRemoteSystem** instance to get an array of **MCDRemoteSystemApplication** objects, which represent apps on the remote device that have been registered to use the Connected Devices Platform (just as you registered your own app in the preliminary steps above). Both **MCDRemoteSystem** and **MCDRemoteSystemApplication** can be used to construct a **MCDRemoteSystemConnectionRequest**, which is what is needed to launch a URI.

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
Depending on the URI that is sent, you can launch an app in a specific state or configuration on a remote device. This allows for the ability to continue a user task, like watching a movie, on a different device without interruption. 

Depending on your use, you may need to cover the cases in which no apps on the targeted system can handle the URI, or multiple apps can handle it. The **[MCDRemoteLauncher](../../../objectivec-api/commanding/MCDRemoteLauncher.md)** class and **[MCDRemoteLauncherOptions](../../../objectivec-api/commanding/MCDRemoteLauncherOptions.md)** class describe how to do this.

### B) Remote app services

Your iOS app can use the Connected Devices Portal interact with app services on other devices. This provides many ways to communicate with other devices&mdash;all without needing to bring an app to the foreground of the host device. 

#### Set up the app service on the target device
This guide will use the [Roman Test App for Windows](http://aka.ms/romeapp) as its target app service. Therefore, the code below will cause an iOS app to look for that specific app service on the given remote system. If you wish to test this scenario, download the Roman Test App on a Windows device and make sure you are signed in with the same MSA or AAD that you used in the preliminary steps above. 

For instructions on how to write your own UWP app service, see [Create and consume an app service (UWP)](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service). You will need to make a few changes in order to make the service compatible with Connected Devices. See the [UWP guide for remote app services](https://docs.microsoft.com/windows/uwp/launch-resume/communicate-with-a-remote-app-service) for instructions on how to do this. 

For instructions on how to set up a host app service on iOS, see the [Hosting guide](../../../hosting/ios/how-to-guides/hosting-ios.md).

#### Open an app service connection on the client device
Your iOS app must acquire a reference to a remote device or application. Like the launch section, this scenario requires the use of a **MCDRemoteSystemConnectionRequest**, which can be constructed from either a **MCDRemoteSystem** or a **MCDRemoteSystemApplication** representing an available app on the system.

Additionally, your app will need to identify its targeted app service by two strings: the *app service name* and *package identifier*. These are found in the source code of the app service provider (see [Create and consume an app service (UWP)](https://msdn.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service) for details). Together these strings construct the **MCDAppServiceDescription**, which is fed into an **MCDAppServiceConnection** instance.

The **MCDAppServiceConnection** uses a **MCDRemoteSystemConnectionRequest** to determine which remote system or app to target, and it uses its internal **MCDAppServiceDescription** to determine the app service. This is necessary because a single app could provide multiple app services. The method below creates an **MCDRemoteSystemConnectionRequest** and then opens the app service connection.

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


#### Create a message to send to the app service

Declare a variable to store the message to send. On iOS, the messages that you send to remote app services will be of the **NSDictionary** type.

> [!NOTE]
> When your app communicates with app services on other platforms, the Connected Devices Platform translates the **NSDictionary** into the equivalent construct on the receiving platform. For example, a **[NSDictionary](https://developer.apple.com/documentation/foundation/nsdictionary)** sent from this app to a Windows app service gets translated into a [**ValueSet**](https://msdn.microsoft.com/library/windows/apps/windows.foundation.collections.valueset) object (of the .NET Framework), which can then be interpreted by the app service. Information passed in the other direction undergoes the reverse translation.

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

> [!IMPORTANT]
> The **NSDictionary** objects that are passed between apps and services in the remote app services scenario must adhere to the following format: Keys must be **NSString**s, and the values may be: **NSString**, boxed numeric types (integers or floating points), boxed booleans, **NSDate**, **NSUUID**, homogeneous arrays of any of these types, or other **NSDictionary** objects that meet this specification. 

#### Send messages to the app service

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

#### Finish app service communication

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
* [API reference page](../api-reference/index.md) 
* [iOS sample app](https://github.com/Microsoft/project-rome/tree/master/iOS/samples) 
* [Communicate with a remote app service (UWP)](https://docs.microsoft.com/windows/uwp/launch-resume/communicate-with-a-remote-app-service)
* [Create and consume an app service (UWP)](https://docs.microsoft.com/windows/uwp/launch-resume/how-to-create-and-consume-an-app-service).
