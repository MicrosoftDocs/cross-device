---
title: MCDAppServiceProvider
description: This protocol contains methods for making a local app service accessible to remote devices.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# protocol `MCDAppServiceProvider`

```
@protocol MCDAppServiceProvider<NSObject> 
```

This protocol contains methods for making a local app service accessible to remote devices. Developers must implement this protocol to make their app services available for remote connectivity.

## Properties 
### appServiceDescription
`@property(nonatomic, readonly, strong, nonnull) MCDAppServiceDescription* appServiceDescription;`

The descriptive information about this app service.

## Methods

### connectionDidOpen
`- (void)connectionDidOpen: (nonnull MCDAppServiceConnection*)connection;`

This method is called when a remote app service connection is opened to this app service.

#### Parameters 
* `connection` The remote app service connection.