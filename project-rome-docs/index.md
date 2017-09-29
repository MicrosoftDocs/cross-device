---
title: Project Rome
description:  "Project Rome" is a project code name for Microsoft's cross-device experiences platform using the Microsoft Graph.
keywords: microsoft, windows, project rome, cross-device, MS Graph, android, ios, xamarin, uwp
---

# Project Rome

"Project Rome" is a project code name for Microsoft's cross-device experiences platform using the Microsoft Graph. This toolkit, consisting of API sets on multiple development platforms, allows an app on a client (local) device to interact with apps and services on a host (remote) device that is signed in with or receptive to the Microsoft Account (MSA) or Azure Active Directory (AAD) account on the client device. This allows developers to program cross-device and cross-platform experiences that are centered around user tasks rather than devices.

Project Rome is currently implemented for the following scenarios. Follow the links for each corresponding section.

[windows-sdk]:             https://developer.microsoft.com/en-us/windows/downloads
[windows-sdk-badge]:       https://img.shields.io/badge/sdk-Creators%20Update-brightgreen.svg?style=flat-square
[windows-sample]:          https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/RemoteSystems
[windows-apps]:            https://github.com/Microsoft/project-rome/tree/master/Windows/samples
[windows-ref]:             https://docs.microsoft.com/uwp/api/windows.system.remotesystems
[windows-docs]:            https://docs.microsoft.com/windows/uwp/launch-resume/connected-apps-and-devices

[xamarin-sdk]:             https://www.nuget.org/packages/Microsoft.ConnectedDevices.Xamarin.Droid
[xamarin-sdk-badge]:       https://img.shields.io/nuget/v/Microsoft.ConnectedDevices.Xamarin.Droid.svg?style=flat-square
[xamarin-sample]:          https://github.com/Microsoft/project-rome/tree/master/Xamarin/samples
[xamarin-docs]:            Xamarin/index.md

[ios-sdk]:                 https://cocoapods.org/?q=ProjectRomeSdk
[ios-sdk-badge]:           https://img.shields.io/cocoapods/v/ProjectRomeSdk.svg?style=flat-square
[ios-sample]:              https://github.com/Microsoft/project-rome/tree/master/iOS/sample 
[ios-ref]:                 iOS/api-reference/index.md
[ios-docs]:                iOS/how-to-guides/index.md

[android-sdk]:             https://bintray.com/projectrome/maven/public_sdk/_latestVersion
[android-sdk-badge]:       https://img.shields.io/bintray/v/projectrome/maven/public_sdk.svg?style=flat-square
[android-sample]:          https://github.com/Microsoft/project-rome/tree/master/Android/sample
[android-ref]:             Android/api-reference/index.md
[android-docs]:            Android/how-to-guides/index.md

[graph-sdk]:               https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview
[graph-sdk-badge]:         https://img.shields.io/badge/REST-Beta-orange.svg?style=flat-square
[graph-sample]:            https://developer.microsoft.com/graph/code-samples-and-sdks
[graph-ref]:               https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview 
[graph-docs]:              https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview

Platform |  Code samples  |     SDK package    | API reference | How-to docs  |
:--------- | :---------- | :----------------: | :------- | :----------- |
Windows | [Windows samples][windows-sample] / [end-to-end apps][windows-apps] |  [![SDK][windows-sdk-badge]][windows-sdk]   | [Windows ref][windows-ref]  | [Windows docs][windows-docs] |
Android | [Android samples][android-sample] | [![Maven][android-sdk-badge]][android-sdk]  | [Android ref][android-ref] | [Android docs][android-docs] |
iOS | [iOS samples][ios-sample]  |     [![CocoaPod][ios-sdk-badge]][ios-sdk]  | [iOS ref][ios-ref]   | [iOS docs][ios-docs]         |
Xamarin | [Xamarin samples][xamarin-sample] |[![Nuget][xamarin-sdk-badge]][xamarin-sdk]   | N/A | [Xamarin docs][xamarin-docs]  |
MS Graph | [MS Graph samples][graph-sample]      |[![REST][graph-sdk-badge]][graph-sdk]            | [Graph ref][graph-ref]      | [Graph docs][graph-docs]  |
