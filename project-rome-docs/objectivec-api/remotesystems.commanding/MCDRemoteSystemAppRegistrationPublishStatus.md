---
title: MCDRemoteSystemAppRegistrationPublishStatus
description: Contains values that describe the status of a remote app launch using a URI.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# enum `MCDRemoteSystemAppRegistrationPublishStatus`

`typedef NS_ENUM(NSInteger, MCDRemoteSystemAppRegistrationPublishStatus)`

Enumeration indicating the status of the publish operation.
The error statuses indicate transient conditions where the app developer may want to retry publishing.

| Name    |Value   |Description   |                  
|------ |------- |--|
|MCDRemoteSystemAppRegistrationPublishStatusSuccess | 0 | Operation completed successfully.|
|MCDRemoteSystemAppRegistrationPublishStatusErrorNoNetwork | 1 | Network was unavailable. |
|MCDRemoteSystemAppRegistrationPublishStatusErrorWebFailure | 2 | A web service failed.|
|MCDRemoteSystemAppRegistrationPublishStatusErrorNoTokenRequestSubscriber | 3 | No token request subscribers responded.|
|MCDRemoteSystemAppRegistrationPublishStatusErrorTokenRequestFailed | 4 | The token request failed.|
|MCDRemoteSystemAppRegistrationPublishStatusErrorAccountNotFound | 5 | Account to publish information for was not found.|
|MCDRemoteSystemAppRegistrationPublishStatusErrorUnknown | 6 | Operation encountered an unknown error.|