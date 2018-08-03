---
title: MCDHostingRemoteSystemApplicationRegistrationBuilder
description: A builder class for MCDHostingRemoteSystemApplicationRegistration instances.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDHostingRemoteSystemApplicationRegistrationBuilder`

```
@interface MCDHostingRemoteSystemApplicationRegistrationBuilder : NSObject 
```

A builder class for **MCDHostingRemoteSystemApplicationRegistration** instances.

## Methods 

### addAttribute
`- (void)addAttribute:(NSString*)value forName : (NSString*)name;`

Add a key/value attribute to the application registration. For example, your app could define a unique ID attribute and share it with client devices. Then they can look for it in subsequent discoveries.

You can change your app's registered attributes by rebuilding an **ApplicationRegistration** with new attributes and re-initializing the Connected Devices Platform, but it is recommended that you keep your attributes constant, possibly adding more as needed when you update your app.

#### Parameters
* `value` The attribute value.
* `name` The name of the attribute.

### addAppServiceProvider
`- (void)addAppServiceProvider:(id<MCDAppServiceProvider>)provider;`

Add an app service provider to the application registration.

#### Parameters
* `provider` The app service provider to add.

### setLaunchUriProvider
`- (void)setLaunchUriProvider:(id<MCDLaunchUriProvider>)provider;`

Set the launch URI provider for the application registration.

#### Parameters
* `provider` The URI provider to add.

### buildRegistration
`- (MCDHostingRemoteSystemApplicationRegistration*)buildRegistration;`

Builds an application registration with the specified properties.

#### Returns
A new MCDHostingRemoteSystemApplicationRegistration instance.