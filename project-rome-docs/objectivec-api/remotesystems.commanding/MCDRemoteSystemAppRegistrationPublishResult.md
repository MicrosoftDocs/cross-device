---
title: MCDRemoteSystemAppRegistrationPublishResult
description: A class communicates the async result of publishing remote system app information for an account.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemAppRegistrationPublishResult` 

```
@interface MCDRemoteSystemAppRegistrationPublishResult : NSObject
```  

This class communicates the async result of publishing remote system app information for an account. The error statuses communicated through this result should be used by the app to retry publishing in the event of certain transient conditions like the network being unavailable.

## Properties

### status
`@property(nonatomic, readonly) MCDRemoteSystemAppRegistrationPublishStatus status;`

Status enum of the publish operation.