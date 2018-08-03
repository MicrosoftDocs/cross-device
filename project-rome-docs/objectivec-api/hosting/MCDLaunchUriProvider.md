---
title: MCDLaunchUriProvider
description: 
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# protocol `MCDLaunchUriProvider`

```
@protocol MCDLaunchUriProvider <NSObject>
```

This class manages the handling of a URI through the launching of an application.

## Properties 
### supportedUriSchemes
`@property(nonatomic, readonly, strong, nonnull) NSArray<NSString*>* supportedUriSchemes;`

An array of strings representing supported URI schemes.

## Methods

### onLaunchUriAsync
`- (void)onLaunchUriAsync:(nonnull NSString*)uri
         withFallbackUri:(nonnull NSString*)fallbackUri
         preferredPackageIds:(nonnull NSArray<NSString*>*)preferredPackageIds
              completion:(nonnull void (^)(BOOL, NSError* _Nullable))completionBlock;`

This method is called when a remote device attempts to launch a URI on this device.

#### Parameters 
* `uri` The URI to launch.
* `fallbackUri` The web-friendly URI to launch in the event that the primary URI fails. This should be a http or https web address or a file.
* `preferredPackageIds` The list of IDs of preferred applications to handle this URI.
* `completionBlock` The code block to execute upon completion.