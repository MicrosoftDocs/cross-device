---
title: MCDRemoteLauncherOptions
description:  A class to represent options for the remote launch feature.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone
---

# class `MCDRemoteLauncherOptions` 

```
@interface MCDRemoteLauncherOptions : NSObject
```  

A class to represent options for the remote launch feature.

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

## Properties

### fallbackUri
`@property(nonatomic, nullable) NSString* fallbackUri;`

The fallback URI to launch on the web in case the app launch URI fails.

### preferredAppIds
`@property(nonatomic, nullable) NSArray<NSString*>* preferredPackageIds;`

A list of **NSString** objects representing IDs of the apps that should be able to launch with this URI. For Windows apps, the ID will be the app's package family name.