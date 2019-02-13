---
title: Microsoft Graph Notifications
description: Include Microsoft Graph notifications in your application to re-engage users in a human-centric way.
ms.localizationpriority: medium
ms.topic: overview
ms.custom: seodec2018
---

# Microsoft Graph Notifications
Notifications are the most effective way to re-engage your users. They can catch your users' attention and bring the user back to your app. In a multi-device world, your users can access your apps and services from anywhere, across different platforms and devices where your apps have a presence.
Your notification scenarios should be designed in a "human-centric" way, in which the primary goal is to notify the user, wherever they are. Existing notification solutions provided by major platforms are excellent at targeting devices. Microsoft Graph notifications improve on this by allowing you to target users. Microsoft Graph notifications will take care of the heavy lifting, including mapping between users and endpoints, syncing notification state across users' different endpoints, and more.

## Why integrate with Microsoft Graph Notifications?

### Deliver notifications to a user across different endpoints
As part of Microsoft Graph, the notifications API allows you to target a Microsoft account, or a work or school (Azure Active Directory) account to deliver a notification. The platform distributes this notification to all the users' endpoints, including Windows UWP, Android, and iOS.

### Manage notifications across endpoints
The Microsoft Graph notifications API allows you to update the state of a notification and sync that state across all endpoints. For example, when a user acts on a notification on one device, you can update the state of this notification (such as marking it as read or dismissed), and the same state change will be distributed to all other endpoints. The Microsoft Graph notifications API tracks the state of your users' notifications in a centralized way, making it easy for you to ensure that your notifications are handled once, and updated or dismissed everywhere.

### Retrieve notification history
You can use the notifications API to retrieve notification history based on an expiration time you define (up to 30 days). Notifications that are marked as read or dismissed are still retrievable from the history, enabling in-app views of notification history and other scenarios.

## Integrating with Microsoft Graph Notifications

### Onboarding
Take a look at the How-To Guide under each platform node (Windows, Android, and iOS) for step-by-step guidance on how to use Graph Notifications as the mobile push notification solution for your apps and services. Note that the how to guides here focus on recieving notifications. You can find information about sending notifications on the [Sending notifications using MS Graph APIs](sending-notifications.md) page.

The guide includes specific steps for using Graph Notifications – including registering cross-platform app identities and mobile push credentials. If you are new to using Microsoft Graph, steps are included for registering your app for Microsoft Account (MSA), for consumer-facing apps) or Azure Active Directory (AAD) for work and school accounts. MSA and AAD are user identities that enable you to take advantage of workloads on Microsoft Graph beyond just notifications, to enable richer business scenarios. 

### Microsoft Graph APIs
When using Graph notifications, the app server is expected to use Microsoft Graph API (beta) to send notifications. For more information on app server-side integration, please see the [API Reference Docs](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/notifications-api-overview) regarding usage of the API. 

### Client-side SDK
To get started with client-side Graph Notifications integration and start receiving and managing notifications using the native SDKs, select your preferred development platform on the left navigation pane. 

* [Sending notifications using MS Graph APIs](sending-notifications.md)
* [Receiving notifications using the Project Rome SDK](receiving-notifications.md)
