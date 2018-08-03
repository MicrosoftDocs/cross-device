---
title: MCDAppServiceDescription
description: This class describes an app service that belongs to a remote device or application.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDAppServiceDescription`

```
@interface MCDAppServiceDescription : NSObject<NSCopying> 
```
This class describes an app service that belongs to a remote device or application.

## Properties 

### name
`@property(nonatomic, readonly, nullable) NSString* name;`

The name of the app service.

### packageId
`@property(nonatomic, readonly, nullable) NSString* packageId;`

The package ID of the app service (equivalent to the package family name on Windows).

## Constructors

### descriptionWithName

`+ (nullable instancetype)descriptionWithName:(nonnull NSString*)name packageId:(nonnull NSString*)packageId;`

#### Parameters 
* `name` The name of the app service being described.
* `packageId` [optional] The package ID of the app service being described.

#### Returns
The initialized [MCDAppServiceDescription](MCDAppServiceDescription.md) if successful, otherwise nil.

### initWithName

`- (nullable instancetype)initWithName:(nonnull NSString*)name packageId:(nonnull NSString*)packageId;`

#### Parameters 
* `name` The name of the app service being described.
* `packageId` [optional] The package ID of the app service being described.

#### Returns
The initialized [MCDAppServiceDescription](MCDAppServiceDescription.md) if successful, otherwise nil.

