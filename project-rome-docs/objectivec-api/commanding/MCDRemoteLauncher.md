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

### launchUri
`- (void)launchUriAsync:(nonnull NSString*)uri withConnectionRequest:(nonnull MCDRemoteSystemConnectionRequest*)connection completion:(nullable void (^)(MCDRemoteLaunchUriStatus result, NSError* _Nullable error))completionBlock;`

Launches a URI against the Remote System specified in an [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md).

#### Parameters
* `uri` The URI which will cause the launching of an app, according to its scheme.
* `connection` Specifies which remote system or application to connect to.
* `completionBlock` The block to invoke upon completion.

### launchUri
`- (void)launchUriAsync:(nonnull NSString*)uri withConnectionRequest:(nonnull MCDRemoteSystemConnectionRequest*)connection options:(nonnull MCDRemoteLauncherOptions*)options completion:(nullable void (^)(MCDRemoteLaunchUriStatus result, NSError* _Nullable error))completionBlock;`

Launches a URI with options against the Remote System specified in an [MCDRemoteSystemConnectionRequest](MCDRemoteSystemConnectionRequest.md).

#### Parameters
* `uri` The URI which will cause the launching of an app, according to its scheme.
* `connection` Specifies which remote system or application to connect to.
* `options` The launch specifications for the app.
* `completionBlock` The block to invoke upon completion.

## Example
The following sample code shows how to use a MCDRemoteLauncher to launch a URI on a remote application

```ObjectiveC
// Send a remote launch of a uri to RemoteSystemApplication
// In the context of the sample app, this method is called with a Button click.
- (IBAction)launchUriButton:(id)sender {
    // get the URI string from elsewhere in application memory
    NSString *uri = self.uriField.text;
    // create a MCDRemoteLauncher instance
    MCDRemoteLauncher* remoteLauncher = [[MCDRemoteLauncher alloc] init];
    // create a connection request with a previously-saved MCDRemoteSystemApplication.
    MCDRemoteSystemConnectionRequest *connectionRequest =
    [MCDRemoteSystemConnectionRequest requestWithRemoteSystemApplication:self.selectedApplication];
    // launch the URI on the given connection
    [remoteLauncher launchUriAsync:uri
        withConnectionRequest:connectionRequest
            completion:^(MCDRemoteLaunchUriStatus result, NSError *_Nullable error) {
                if (error) {
                    // handle the error case
                    NSLog(@"LaunchURI [%@]: ERROR: %@", uri, error);
                    return;
                }
                
                if (result == MCDRemoteLaunchUriStatusSuccess) {
                    // handle the success case
                    NSLog(@"LaunchURI [%@]: Success!", uri);
                }
                else {
                    // handle the case of a non-success status
                    NSLog(@"LaunchURI [%@]: Failed with code %d", uri, (int)result);
                }
            }];
}
```