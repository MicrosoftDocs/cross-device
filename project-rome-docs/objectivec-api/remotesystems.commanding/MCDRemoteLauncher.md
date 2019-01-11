---
title: MCDRemoteLauncher
description: A class used to launch an app on a remote device using a URI.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteLauncher` 

```
@interface MCDRemoteLauncher : NSObject
```  

A class used to launch an app on a remote device using a URI.


## Methods

### launchUriAsync
```
- (void)launchUriAsync:(nonnull NSString*)uri
 withConnectionRequest:(nonnull MCDRemoteSystemConnectionRequest*)connection
            completion:(nullable void (^)(MCDRemoteLaunchUriStatus result, NSError* _Nullable error))completionBlock;
```

Launches a URI against the Remote System specified in an [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md).

#### Parameters
* `uri` The URI which will cause the launching of an app, according to its scheme.
* `connection` Specifies which remote system or application to connect to.
* `completionBlock` The block to invoke upon completion.

### launchUriAsync
```
- (void)launchUriAsync:(nonnull NSString*)uri
 withConnectionRequest:(nonnull MCDRemoteSystemConnectionRequest*)connection
               options:(nullable MCDRemoteLauncherOptions*)options
            completion:(nullable void (^)(MCDRemoteLaunchUriStatus result, NSError* _Nullable error))completionBlock;
```

Launches a URI with options against the Remote System specified in an [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md).

#### Parameters
* `uri` The URI which will cause the launching of an app, according to its scheme.
* `connection` Specifies which remote system or application to connect to.
* `options` The launch specifications for the app.
* `completionBlock` The block to invoke upon completion.