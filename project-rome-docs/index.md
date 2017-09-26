# Project Rome

"Project Rome" is a project code name for Microsoft's cross-device experiences platform using the Microsoft Graph. This toolkit, consisting of API sets on multiple development platforms, allows an app on a client (local) device to interact with apps and services on a host (remote) device that is signed in with or receptive to the Microsoft Account (MSA) or Azure Active Directory (AAD) account on the client device. This allows developers to program cross-device and cross-platform experiences that are centered around user tasks rather than devices.

Project Rome is currently implemented for the following scenarios. Follow the links for each corresponding section.

[windows-sdk]:             https://developer.microsoft.com/en-us/windows/downloads
[windows-sdk-badge]:       https://img.shields.io/badge/sdk-Creators%20Update-brightgreen.svg?style=flat-square
[windows-sample]:          https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/RemoteSystems
[windows-ref]:             https://docs.microsoft.com/uwp/api/windows.system.remotesystems
[windows-docs]:            https://docs.microsoft.com/en-us/windows/uwp/launch-resume/connected-apps-and-devices

[xamarin-sdk]:             https://www.nuget.org/packages/Microsoft.ConnectedDevices.Xamarin.Droid
[xamarin-sdk-badge]:       https://img.shields.io/nuget/v/Microsoft.ConnectedDevices.Xamarin.Droid.svg?style=flat-square
[xamarin-sample]:          https://github.com/Microsoft/project-rome/tree/master/Xamarin/samples

[ios-sdk]:                 https://cocoapods.org/?q=ProjectRomeSdk
[ios-sdk-badge]:           https://img.shields.io/cocoapods/v/ProjectRomeSdk.svg?style=flat-square
[ios-sample]:              https://github.com/Microsoft/project-rome/tree/master/iOS/sample 
[ios-ref]:                 iOS/api-reference/
[ios-docs]:                TBD

[android-sdk]:             https://bintray.com/projectrome/maven/public_sdk/_latestVersion
[android-sdk-badge]:       https://img.shields.io/bintray/v/projectrome/maven/public_sdk.svg?style=flat-square
[android-sample]:          https://github.com/Microsoft/project-rome/tree/master/Android/sample
[android-ref]:             Android/api-reference/
[android-docs]:            TBD

[graph-sdk]:               https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview
[graph-sdk-badge]:         https://img.shields.io/badge/REST-Beta-orange.svg?style=flat-square
[graph-sample]:            https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview
[graph-ref]:               MSGraph/ 
[graph-docs]:              TBD

|  Code samples  |     SDK package    | API reference | How-to docs  |
| :------------- | :----------------: | :------- | :----------- |
| **[Windows][windows-sample]**           |  [![SDK][windows-sdk-badge]][windows-sdk]       | [ref][windows-ref]  | [docs][windows-docs] |
| **[Android][android-sample] (Preview)** | [![Maven][android-sdk-badge]][android-sdk]      | [ref][android-ref]  | [docs]
| **[iOS][ios-sample] (Preview)**         |     [![CocoaPod][ios-sdk-badge]][ios-sdk]       | [ref][ios-ref]      | [docs]
| **[Xamarin for Android][xamarin-sample] (Preview)** |[![Nuget][xamarin-sdk-badge]][xamarin-sdk] | Coming Soon   | [docs]
| **[MSGraph][graph-sample] (Preview)**   |[![REST][graph-sdk-badge]][graph-sdk]            | [ref][graph-ref]    | [docs]
