---
title: MCDRemoteSystemApp
description: Represents an application on a remote system that is available for connectivity.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemApp` 

```
@interface MCDRemoteSystemApp : NSObject
```  

Represents an application on a remote system that is available for connectivity.

## Properties

### appId
`@property(nonatomic, readonly, nonnull) NSString* appId;`

A unique identifier for this application.

### displayName
`@property(nonatomic, readonly, nonnull) NSString* displayName;`

The friendly display name for this application. This is the name used by the device for Bluetooth identification. If this hasn't been set or the device doesn't support Bluetooth, this field will be empty.

### availableByProximity
`@property(nonatomic, readonly, getter=isAvailableByProximity) BOOL availableByProximity;`

Indicates whether this application is currently available for proximal connection.

### availableBySpatialProximity
`@property(nonatomic, readonly, getter=isAvailableBySpatialProximity) BOOL availableBySpatialProximity;`

Indicates whether this application is currently available for spatial sharing connection.

### attributes
`@property(nonatomic, readonly, nonnull) NSDictionary<NSString*, NSString*>* attributes;`

A dictionary of key/value pairs defining the attributes of this application.

### appServices
`@property(nonatomic, readonly, nullable) NSArray<MCDAppServiceDescription*>* appServices;`

An array of MCDAppServiceDescription instances describing the app services that this application provides for remote connectivity.

### accounts
`@property(nonatomic, readonly, nullable) NSArray<MCDConnectedDevicesAccount*>* accounts;`

TODO