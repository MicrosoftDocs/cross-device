---
title: MCDRemoteSystemApplicationRegistration
description: This class represents an application. A registered app can provide remote app services or be used to launch a URI.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDRemoteSystemApplicationRegistration`

```
@interface MCDHostingRemoteSystemApplicationRegistration : MCDRemoteSystemApplicationRegistration
```

This class represents an application. A registered app can provide remote app services or be used to launch a URI.

## Properties 

### appServiceProviders
`@property(nonatomic, readonly, nullable) NSArray<id<MCDAppServiceProvider>>* appServiceProviders;`

An array of app services that this application can expose for remote connectivity.

### launchUriProvider
`@property(nonatomic, readonly, nullable) id<MCDLaunchUriProvider> launchUriProvider;`

The provider of URI launch functionality for this application.