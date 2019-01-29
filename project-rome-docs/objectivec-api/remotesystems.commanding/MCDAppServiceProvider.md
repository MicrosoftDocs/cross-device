---
title: MCDAppServiceProvider
description: This protocol contains methods for making a local app service accessible to remote devices.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# protocol `MCDAppServiceProvider`

```
@protocol MCDAppServiceProvider<NSObject>
```

This protocol contains methods for making a local app service accessible to remote devices. Developers must implement this protocol to make their app services available for remote connectivity.

## Properties
 
### appServiceInfo
`@property(nonatomic, readonly, strong, nonnull) MCDAppServiceInfo* appServiceInfo;`

The descriptive information about this app service.

## Methods

### connectionDidOpen
`- (void)connectionDidOpen:(nonnull MCDAppServiceConnectionOpenedInfo*)openedInfo;`

This method is called when a remote app service connection is opened to this app service.

#### Parameters 
* `openedInfo`

A MDCAppServiceConnectionOpenedInfo instance containing information for remote messaging with the app service.