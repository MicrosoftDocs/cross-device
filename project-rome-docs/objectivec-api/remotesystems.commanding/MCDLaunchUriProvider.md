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
`@property(nonatomic, readonly, strong, nullable) NSArray<NSString*>* supportedUriSchemes;`

An array of strings representing supported URI schemes.

## Methods

### onLaunchUriAsync
```
- (void)onLaunchUriAsync:(nonnull NSString*)uri
         options:(nullable MCDRemoteLauncherOptions*)options
              completion:(nonnull void (^)(BOOL, NSError* _Nullable))completionBlock;
```

This method is called when a remote device attempts to launch a URI on this device.

#### Parameters 
* `uri` The URI to launch.
* `options` A set of options for launching the URI. The fallback URI is only one of the possible options that can be set.
* `completionBlock` The code block to execute upon completion.