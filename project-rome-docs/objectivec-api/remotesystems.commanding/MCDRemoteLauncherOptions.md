---
title: MCDRemoteLauncherOptions
description:  A class to represent options for the remote launch feature.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteLauncherOptions` 

```
@interface MCDRemoteLauncherOptions : NSObject
```  

A class to represent options for the remote launch feature.

## Properties

### fallbackUri
`@property(nonatomic, copy, nullable) NSString* fallbackUri;`

The fallback URI to launch on the web in case the app launch URI fails.

### preferredPackageIds
`@property(nonatomic, copy, nullable) NSArray<NSString*>* preferredPackageIds;`

A list of **NSString** objects representing IDs of the apps that should be able to launch with this URI. For Windows apps, the ID will be the app's package family name.

## Constructors

### optionsWithFallbackUri
`+ (nullable instancetype)optionsWithFallbackUri: (nullable NSString*)fallbackUri  preferredPackageIds: (nullable NSArray<NSString*>*)preferredPackageIds;`

#### Parameters
* `fallbackUri` The fallback URI to launch on the web in case the app launch URI fails.
* `preferredPackageIds` A list of **NSString** objects representing IDs of the apps that should be able to launch with this URI. For Windows apps, the ID will be the app's package family name.

#### Returns
The initialized [MCDRemoteLauncherOptions](MCDRemoteLauncherOptions.md) if successful, otherwise nil.

### initWithFallbackUri
`- (nullable instancetype)initWithFallbackUri:(nullable NSString*)fallbackUri preferredPackageIds:(nullable NSArray<NSString*>*)preferredPackageIds;`

#### Parameters
* `fallbackUri` The fallback URI to launch on the web in case the app launch URI fails.
* `preferredPackageIds` A list of **NSString** objects representing IDs of the apps that should be able to launch with this URI. For Windows apps, the ID will be the app's package family name.

#### Returns
The initialized [MCDRemoteLauncherOptions](MCDRemoteLauncherOptions.md) if successful, otherwise nil.