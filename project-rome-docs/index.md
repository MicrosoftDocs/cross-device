---
title: Build Cross-Device Applications
description: Learn about the cross-device and cross-platform features enables for Windows 10 applications using Project Rome.
ms.topic: overview
ms.custom: "seodec2018, RS5"
---
# Project Rome

[Project Rome](https://developer.microsoft.com/en-us/windows/project-rome) is a platform for creating multi-device, multi-platform applications, with the goal of creating human-centric scenarios that move with the user regardless of form factor or platform.

Project Rome consists of a set of cross-device and cross-platform features that developers can use to increase engagement in their apps and create experiences that center around people and their tasks rather than devices. The programming model comes in the form of API sets for Windows, Android, iOS, and Microsoft Graph. Both client and server-side applications can utilize Project Rome capabilities.

On this site you will find developer documentation for the Project Rome SDKs. Select a feature on the left navigation pane to get started. Additionally, you can visit the [Project Rome landing page](https://developer.microsoft.com/windows/project-rome) for more general information, or see the [Project Rome samples repo](https://github.com/Microsoft/project-rome) for sample apps that showcase these features.

Some scenarios are available through both the native platform SDKs and through REST APIs (Microsoft Graph), which can be called from any device capable of making HTTP requests. In order to decide which implementation is right for your app, consider the following:

* The platform SDKs provide an object model in the native language, local storage, and a publish-subscribe pattern to update the app when server-side information changes.
* If your app runs on Windows (UWP or Win32 apps), the platform SDK provides a number of additional features, such as using the users' default account and automatically tracking user engagement. 
*  If you plan to use other Project Rome features that are only available through the platform SDKs, you may wish to implement each of the features in the same way.
* Use the Microsoft Graph REST APIs for a quicker and simpler implementation if you don't require the scenarios above.

Some other scenarios are enabled by using a combination of Microsoft Graph APIs and client SDKs. An example of this is Notifications. In this case, MS Graph API is used to publish notifications from app server side, and the native-platform client SDKs are utilized to receive and manage notifications in each client-side native apps. 
