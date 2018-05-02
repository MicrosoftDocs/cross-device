---
title: Project Rome with Xamarin on Android (preview release)
description:  Getting started with the Project Rome plugin for Xamarin on Android.
keywords: microsoft, windows, project rome, how-to Xamarin, xamarin on android 
---

# Getting started with the Project Rome plugin for Xamarin on Android

This plugin allows you to access the Project Rome Connected Devices APIs on Android while programming in the Xamarin environment. As with the native Android SDK, you use this plugin with Xamarin to discover, launch apps, and send messages to Windows devices and applications from your Android application.

## Setup

First, be sure you have a development environment that supports Xamarin: Visual Studio 2015 or 2017 RC with Xamarin or Xamarin Studio. For information on getting started with Xamarin in general,see the official [Xamarin guides](https://developer.xamarin.com/guides/).

Next, install the latest version of the plugin.

|Platform|Supported|Compatible versions|
| :------------------- | :----------- | :------------------ |
|[Xamarin.Android](https://www.nuget.org/packages/Microsoft.ConnectedDevices.Xamarin.Droid)|Yes|API 19+|

Create a new application and register it on the [Microsoft Developer Portal](https://apps.dev.microsoft.com) to obtain an MSA client ID.

## API usage

The following code examples show how to utilize the essential features of Project Rome for Android apps written with Xamarin.

### Initialize the Connected Devices Platform.

```csharp
// CLIENT_ID is the previously acquired MSA client ID.
Platform.FetchAuthCode += Platform_FetchAuthCode;
var result = await Platform.InitializeAsync(this.ApplicationContext, CLIENT_ID);
```

The `Platform_FetchAuthCode` method is called by the platform when it needs an authorization code from the user. See the sample for a more detailed usage.

```csharp
private async void Platform_FetchAuthCode(string oauthUrl)
{
    var authCode = await AuthenticateWithOAuth(oauthUrl);
    Platform.SetAuthCode(token);
}
```

### Discover devices
To discover remote devices, do the following.

```csharp
// Use a RemoteSystemWatcher instance to discover devices.
private RemoteSystemWatcher _remoteSystemWatcher;
private void DiscoverDevices()
{
    _remoteSystemWatcher = RemoteSystem.CreateWatcher();
    _remoteSystemWatcher.RemoteSystemAdded += (sender, args) =>
    {
        // print the discovered device to the console
        Console.WriteLine("Discovered Device: " + args.P0.DisplayName);
    };
    // Begin device discovery
    _remoteSystemWatcher.Start();
}
```

### Remote launch
Finally, connect and launch apps on remote devices through the use of URIs.

```csharp
private async void RemoteLaunchUri(RemoteSystem remoteSystem, Uri uri)
{
    var launchUriStatus = await RemoteLauncher.LaunchUriAsync(new RemoteSystemConnectionRequest(remoteSystem), uri);
}
```

