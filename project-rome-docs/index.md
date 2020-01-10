---
title: Build Cross-Device Applications
description: Learn about the cross-device and cross-platform features enables for Windows 10 applications using Project Rome.
ms.topic: overview
ms.custom: "seodec2018, RS5"
---

# Project Rome

[Project Rome](https://developer.microsoft.com/windows/project-rome) is Microsoft's cross-device experiences platform for apps. 

On this site you will find developer documentation for Project Rome and links to other useful resources.

For news, blog posts, and videos about Project Rome, visit the [Project Rome landing page](https://developer.microsoft.com/windows/project-rome).

For sample applications using Project Rome, check out the SDK table below, or visit the [Project Rome samples repo](https://github.com/Microsoft/project-rome).

## About Project Rome

Project Rome allows developers to write apps that can run on multiple devices and travel with the user as they switch between devices.

Project Rome includes features exposed via Microsoft Graph and platform-specific native SDKs. These features enable multiple cross-device and connected-device capabilities, allowing your apps to be centralized around a logged-in user identity. Features associated with Project Rome include but are not limited to user activities, notifications, device relay, and nearby share.

## Choosing between native APIs and Graph APIs

Some scenarios are available through *both* the native platform SDKs and REST APIs via Microsoft Graph. In general, the REST APIs enable quick and simple implementation of the Project Rome features. However, there are some advantages to using platform-specific implementations:

* The platform SDKs provide an object model in the native language, local storage, and a publish-subscribe pattern to update the app when server-side information changes.
* If your app runs on Windows (UWP or Win32 apps), the platform SDK provides a number of additional features, such as using the users' default account and automatically tracking user engagement.
* If you plan to use other Project Rome features that are only available through the platform SDKs, you may wish to implement each of the features in the same way.

Some other scenarios are enabled by using a combination of Microsoft Graph APIs and client SDKs. An example of this is Notifications. In this case, MS Graph API is used to publish notifications from app server side, and the native-platform client SDKs are utilized to receive and manage notifications in each client-side native apps.

## SDK

Project Rome is currently implemented for the below platforms. Follow the links for samples and SDK downloads.

[windows-sdk]:             https://developer.microsoft.com/windows/downloads
[windows-sdk-badge]:       https://img.shields.io/badge/sdk-April%202018%20Update-brightgreen.svg
[windows-drsample]:        https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/RemoteSystems
[windows-afsample]:        https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/UserActivity 

[winredist-sdk]:           https://www.nuget.org/packages/Microsoft.ConnectedDevices.UserNotifications
[winredist-sdk-badge]:     https://img.shields.io/nuget/v/Microsoft.ConnectedDevices.UserNotifications.svg
[winredist-sample]:        https://github.com/microsoft/project-rome/tree/master/Windows/samples

[xamarin-sdk]:             https://www.nuget.org/packages/Microsoft.ConnectedDevices.Xamarin.Droid
[xamarin-sdk-badge]:       https://img.shields.io/nuget/v/Microsoft.ConnectedDevices.Xamarin.Droid.svg
[xamarin-sample]:          https://github.com/Microsoft/project-rome/tree/0.8.1/Xamarin/samples

[ios-sdk]:                 https://cocoapods.org/pods/ProjectRomeSdk
[ios-sdk-badge]:           https://img.shields.io/cocoapods/v/ProjectRomeSdk.svg
[ios-sample]:              https://github.com/microsoft/project-rome/tree/master/iOS/samples

[android-sdk]:             https://bintray.com/connecteddevices/maven/com.microsoft.connecteddevices%3Aconnecteddevices-sdk/_latestVersion
[android-sdk-badge]:       https://api.bintray.com/packages/connecteddevices/maven/com.microsoft.connecteddevices%3Aconnecteddevices-sdk/images/download.svg
[android-sample]:          https://github.com/microsoft/project-rome/tree/master/Android/samples

[graph-relay]:             https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview
[graph-activities]:        https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/activity-feed-api-overview
[graph-notification]:      https://developer.microsoft.com/graph/docs/api-reference/beta/resources/notifications-api-overview

[graph-relay-badge]:       https://img.shields.io/badge/Device_Relay-Beta-orange.svg
[graph-activities-badge]:  https://img.shields.io/badge/Activities-1.0-brightgreen.svg
[graph-notification-badge]:https://img.shields.io/badge/Graph_Notifications-Beta-orange.svg

[graph-relay-sample]:        https://developer.microsoft.com/graph/docs/api-reference/beta/resources/project_rome_overview
[graph-activities-sample]:   https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/activity-feed-api-overview
[graph-notification-sample]: https://developer.microsoft.com/graph/docs/api-reference/beta/resources/notifications-api-overview



|   Platform                        | Features                                                         |           SDK Package                          |   Samples                                       |
| :-------------------------------- | :--------------------------------------------------------------- |:---------------------------------------------- | :---------------------------------------------- |
| **Windows SDK**                   | Device Relay, Activities/Timeline                                | [![SDK][windows-sdk-badge]][windows-sdk]       | [Project Rome for Device Relay Windows sample][windows-drsample] <br> [Project Rome for Activities Windows sample][windows-afsample]
| **Windows (Preview)**             |                                    Microsoft Graph Notifications | [![Nuget][winredist-sdk-badge]][winredist-sdk] | [Graph Notifications for Windows sample][winredist-sample] 
| **Android**             | Device Relay, Activities/Timeline, Microsoft Graph Notifications (Preview) | [![Maven][android-sdk-badge]][android-sdk]     | [Project Rome for Android sample][android-sample]
| **iOS**                 | Device Relay, Activities/Timeline, Microsoft Graph Notifications (Preview) | [![CocoaPod][ios-sdk-badge]][ios-sdk]          | [Project Rome for iOS sample][ios-sample]
| **Xamarin for Android (Preview)** | Device Relay                                                     | [![Nuget][xamarin-sdk-badge]][xamarin-sdk]     | [Xamarin for Android sample][xamarin-sample]
| **MSGraph**                       | Device Relay, Activities/Timeline, Microsoft Graph Notifications | [![REST][graph-relay-badge]][graph-relay]<br> [![REST][graph-activities-badge]][graph-activities]<br>[![REST][graph-notification-badge]][graph-notification]          | [Device Relay][graph-relay-sample]<br>[Activities/Timeline][graph-activities-sample]<br>[Graph Notifications][graph-notification-sample]

## Project Rome blog posts
* [Cross-device experiences with Project Rome](https://blogs.windows.com/buildingapps/2016/10/11/cross-device-experience-with-project-rome/#iQTseFlAMJRopU9k.97)

* [Going social: Project Rome, Maps, & Social Network Integration](https://blogs.windows.com/buildingapps/2016/10/27/going-social-project-rome-maps-social-network-integration-app-dev-on-xbox-series/#SCfoEZ1q8c1yBMei.97)

* [Announcing Project Rome Android SDK](https://blogs.windows.com/buildingapps/2017/02/08/announcing-project-rome-android-sdk/#obDkvwkXOGa3tcTx.97)

* [Project Rome for Android Update: Now with App Services Support](https://blogs.windows.com/buildingapps/2017/03/23/project-rome-android-update-now-app-services-support/#DBm1Ic4JX8vXv2h0.97)

* [Building a Remote Control Companion App for Android with Project Rome](https://devblogs.microsoft.com/xamarin/building-remote-control-companion-app-android-project-rome/)

* [New Share Experience in Windows 10 Creators Update](https://blogs.windows.com/buildingapps/2017/04/06/new-share-experience-windows-10-creators-update/#OGskrWcLLlrCTCSH.97)

* [Web-to-App Linking with AppUriHandlers](https://blogs.windows.com/buildingapps/2016/10/14/web-to-app-linking-with-appurihandlers/#fIh7USaxBYS8JqfT.97)

## Other resources

* [Web-to-app linking](https://docs.microsoft.com/windows/uwp/launch-resume/web-to-app-linking)

* [//Build 2016 talk](https://channel9.msdn.com/Events/Build/2016/B831)

* [MS Dev Show podcast](http://msdevshow.com/2016/11/project-rome-with-shawn-henry/)

## Give feedback

|[UserVoice](https://wpdev.uservoice.com/forums/110705-universal-windows-platform/category/183208-connected-apps-and-devices-project-rome)|[Feedback Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)|[Contact Us](mailto:projectrometeam@microsoft.com)|
|-----|-----|-----|
