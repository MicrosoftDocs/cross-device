---
title: MCDAppServiceInfo
description: This class describes an app service that belongs to a remote device or application.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDAppServiceInfo` 

```
@interface MCDAppServiceInfo : NSObject<NSCopying>
```  

This class describes an app service that belongs to a remote device or application.

## Properties

### name
`@property(nonatomic, readonly, nullable) NSString* name;`

The name of the app service being described.

### packageId
`@property(nonatomic, readonly, nullable) NSString* packageId;`

The package ID of the app service being described.

## Constructors

### infoWithName
`+ (nullable instancetype)infoWithName:(nonnull NSString*)name;`

Initialize the class with the name of the app service.

#### Parameters 
* `name` 

The name of the app service being described.

#### Returns
A new instance of this class with app service name.

### infoWithName
`- (nullable instancetype)infoWithName:(nonnull NSString*)name;`

TODO

#### Parameters 
* `name` 

TODO

#### Returns
TODO

### infoWithName
`+ (nullable instancetype)infoWithName:(nonnull NSString*)name packageId:(nonnull NSString*)packageId;`

Initialize the class with the name of the app service.

#### Parameters 
* `name` 

The name of the app service being described.

* `packageId` 

The package ID of the app service being described.

#### Returns
A new instance of this class with app service name and packageId.

### infoWithName
`- (nullable instancetype)infoWithName:(nonnull NSString*)name packageId:(nonnull NSString*)packageId;`

TODO

#### Parameters 
* `name` 

TODO

* `packageId` 

TODO

#### Returns
TODO
