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

Initialize the class with information and name of the app service.

#### Parameters 
* `name` 

The name of the app service being described.

#### Returns
Returns an MCDAppServiceInfo object containing the provided name.

### initWithName
`- (nullable instancetype)initWithName:(nonnull NSString*)name;`

Initialize the class with the name of the app service.

#### Parameters 
* `name` 

The name of the app service being described.

#### Returns
Returns an MCDAppServiceInfo object initialized with the provided name.

### infoWithName
`+ (nullable instancetype)infoWithName:(nonnull NSString*)name packageId:(nonnull NSString*)packageId;`

Initialize the class with information and name of the app service.

#### Parameters 
* `name` 

The name of the app service being described.

* `packageId` 

The package ID of the app service being described.

#### Returns
Returns an MCDAppServiceInfo object containing the provided name.

### initWithName
`- (nullable instancetype)initWithName:(nonnull NSString*)name packageId:(nonnull NSString*)packageId;`

Initialize the class with the name of the app service.

#### Parameters 
* `name` 

The name of the app service being described.

* `packageId` 

The package ID of the app service being described.

#### Returns
Returns an MCDAppServiceInfo object initialized with the provided name.
