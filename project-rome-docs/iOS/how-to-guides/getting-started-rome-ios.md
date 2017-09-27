# Getting started with Connected Devices (iOS)
This guide shows you how to remotely launch a Universal Windows Platform (UWP) app or Windows desktop app on a Windows device from an app on an iOS device. Refer to the [iOS sample app](https://github.com/Microsoft/project-rome/tree/master/iOS/sample) for a working example.

Remote app launching can be useful when the user wishes to start a task on one device and finish it on another. For example, you might receive a Skype call on your Android phone and later wish to launch the Skype app on your desktop PC to continue the call there. Note, however, that the client's and host's apps do not need to be the same: your iOS app can launch any Windows app on a connected Windows device.

Remote launch is achieved by sending a Uniform Resource Identifier (URI) from one device to another. A URI specifies a *scheme*, which determines which app(s) can handle its information. See [Launch the default app for a URI](https://msdn.microsoft.com/windows/uwp/launch-resume/launch-default-app) for information on using URIs to launch Windows apps.

## Preliminary setup for Connected Devices functionality

Before implementing device discovery and connectivity, there are a few steps you'll need to take to give your iOS app the capability to connect to remote Windows devices.

First, you must register your app with Microsoft by following the instructions on the [Microsoft developer portal](https://apps.dev.microsoft.com/). This will allow your app to access Microsoft's Connected Devices platform by having users sign in to their Microsoft accounts (MSAs). You will receive a client ID which you'll use to authenticate your app. To do this in the [sample](https://github.com/Microsoft/project-rome/tree/master/iOS/sample) app, replace the value of _appId_ in _AuthenticationViewController.m_ with this value.

The simplest way to add the Connected Devices platform to your iOS app is by using the [CocoaPods](https://cocoapods.org/) dependency manager. Go to your iOS project's *Podfile* and insert the following entry:

```Objective-C
platform :ios, '10.0'

target 'ProjectName' do
  pod 'ProjectRomeSdk', '~>0.0.3'
end
```

You can also download and install versions of the iOS SDK manually from the [binaries folder](https://github.com/Microsoft/project-rome/tree/master/iOS/binaries).

See the [sample app](https://github.com/Microsoft/project-rome/tree/master/iOS/sample) for proper usage of the core Connected Devices APIs for iOS.

## Known issues

As this is a preview release, there are some known bugs in the Connected Devices platform for iOS.

|Description | Workaround |
| -----|-----|
|Discovery may stop working if the application has been running for over an hour. | Reinitialize the platform by calling **CDPlatform::shutdown** and then **CDPlatform::initWithOAuthCodeProviderDelegate** |
|Devices may connect over the cloud and not proximally (if available) on first discovery. | Initiate another discovery using **CDRemoteSystemDiscovery**. |
| You will receive a linker error regarding bit code in your new project. | Disable bitcode by selecting your project and going to Build Settings -> All -> Enable Bitcode|
|  Any consuming app's documents on drive will grow monotonically in size over time.| No current workaround.|
|App crashes without **CFBundleDisplayName** entry.|Create a **CFBundleDisplayName** entry in your _Info.plist_ file.|
|Connected Devices framework includes simulator (x86, x86_64) slices which will fail App Store ingestion. | Remove using lipo|
