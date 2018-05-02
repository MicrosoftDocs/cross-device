---
title: MCDRemoteSystemApplication
description: Represents an application on a remote system that is available for connectivity.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteSystemApplication` 

```
@interface MCDRemoteSystemApplication : NSObject
```  

Represents an application on a remote system that is available for connectivity.

## Properties

### applicationId
`@property(nonatomic, readonly, nonnull) NSString* applicationId;`

A unique identifier for this application.

### displayName
`@property(nonatomic, readonly, nonnull) NSString* displayName;`

The friendly display name for this application.

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
