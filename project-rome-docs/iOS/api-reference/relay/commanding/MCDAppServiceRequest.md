---
title: MCDAppServiceRequest
description:  Represents an incoming message from a remote app/device to this app service connection.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDAppServiceRequest`

```
@interface MCDAppServiceRequest : NSObject
```

Represents an incoming message from a remote app/device to this app service connection.

## Properties

### message 
`@property(nonatomic, readonly, nonnull) NSDictionary* message;`

The message for the remote app service.

## Methods

### sendResponseAsync 
`- (void)sendResponseAsync:(nonnull NSDictionary*)message completion:(nonnull void (^)(MCDAppServiceResponseStatus, NSError* _Nullable))completion;`

Sends a response message to the remote app service that sent the request.

#### Parameters
* `message` The message for the remote app service.

## Example
The following sample code uses an [MCDAppServiceConnection](MCDAppServiceConnection.md) and related classes to connect to a remote app service and exchange a simple message to compare date information and get the total delivery time.

```Objective-C
MCDAppServiceConnection *_appServiceConnection;
NSUInteger _requestReceivedRegistration;
NSUInteger _serviceClosedRegistration;
NSDateFormatter *_dateFormatter;

// ...

// Establish an app service connection
- (IBAction)connectAppServiceButton:(id)sender {
    MCDAppServiceConnection* connection = nil;
    @synchronized(self) {
        connection = _appServiceConnection;
        if (!connection) {
            // create a new MCDAppServiceConnection object
            connection = _appServiceConnection = [MCDAppServiceConnection new];
            // set a description with previously-defined strings
            connection.appServiceDescription =
            [MCDAppServiceDescription descriptionWithName:g_appServiceName packageId:g_packageIdentifier];
            // add the service closed listener (method defined below)
            _serviceClosedRegistration =
            [connection addServiceClosedListener:^(__unused MCDAppServiceConnection* connection, MCDAppServiceClosedStatus status) {
                [self appServiceConnection:connection closedWithStatus:status];
            }];
        }
    }
    
    @try {
        MCDRemoteSystemConnectionRequest *connectionRequest =
        [MCDRemoteSystemConnectionRequest requestWithRemoteSystemApplication:self.selectedApplication];
        [connection openRemoteAsync:connectionRequest
                         completion:^(MCDAppServiceConnectionStatus status, NSError* error) {
                             if (error) {
                                 NSLog(@"ConnectAppService: ERROR: %@", error);
                                 return;
                             }
                             if (status != MCDAppServiceConnectionStatusSuccess) {
                                 NSLog(@"ConnectAppService: Failed with code %d", (int)status);
                                 return;
                             }
                             NSLog(@"Successfully connected!");
                             dispatch_async(dispatch_get_main_queue(), ^{ self.appServiceStatusLabel.text = @"App service connected! no ping sent"; });
                         }];
    }
    @catch (NSException* ex) {
        NSLog(@"ConnectAppService: EXCEPTION! %@", ex);
    }
}

// Create a message to send
- (NSDictionary*)_createPingMessage {
    return @{
        @"Type" : @"ping",
        @"CreationDate" : [_dateFormatter stringFromDate:[NSDate date]],
        @"TargetId" : _selectedApplication.applicationId
    };
}

// Send a message using the app service connection
- (IBAction)sendAppServiceButton:(id)sender {
    if (!_appServiceConnection) {
        return;
    }
    
    // Send the message and get a response
    @try {
        [_appServiceConnection sendMessageAsync:[self _createPingMessage]
            completion:^(MCDAppServiceResponse *response, NSError* error) {
                if (error) {
                    NSLog(@"SendPing: ERROR: %@", error);
                    return;
                }
                
                if (response.status != MCDAppServiceResponseStatusSuccess) {
                    NSLog(@"SendPing: Response received with bad status code %d", (int)response.status);
                    return;
                }
                
                NSString* creationDateString = response.message[@"CreationDate"];
                if (creationDateString) {
                    NSDate* date = [_dateFormatter dateFromString:creationDateString];
                    if (date)
                    {
                        NSTimeInterval diff = [[NSDate date] timeIntervalSinceDate:date];
                        dispatch_async(dispatch_get_main_queue(),
                                    ^{ self.appServiceStatusLabel.text = [NSString stringWithFormat:@"%g", diff]; });
                    }
                }
            }];
    }
    @catch (NSException* ex) {
        NSLog(@"SendPing: EXCEPTION! %@", ex);
    }
}


// define the app service closed listener
- (void)appServiceConnection:(__unused MCDAppServiceConnection*)connection closedWithStatus:(MCDAppServiceClosedStatus)status {
    NSLog(@"AppService closed with status %d", (int)status);
    dispatch_async (
        dispatch_get_main_queue(), ^{ self.appServiceStatusLabel.text = [NSString stringWithFormat:@"disconnected (%d)", (int)status]; });
}
```
