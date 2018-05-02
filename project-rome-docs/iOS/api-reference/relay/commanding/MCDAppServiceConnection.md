---
title: MCDAppServiceConnection
description:  This class manages a connection to a particular remote app service.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDAppServiceConnection`

```
@interface MCDAppServiceConnection : NSObject
```

This class manages a connection to a particular remote app service.

## Properties

### request 
`@property(nonatomic, readonly, nonnull) MCDAppServiceRequest* request;`

The connection request associated with the target device.

### appServiceDescription
`@property(nonatomic, copy, nonnull) MCDAppServiceDescription* appServiceDescription;`

Provides details about the target app service to connect to.

## Constructors

### init
`- (nullable instancetype)init;`

#### Returns
The initialized [MCDAppServiceConnection](MCDAppServiceConnection.md) if successful, otherwise nil.

### initWithConnectionRequest 
`- (nullable instancetype)initWithAppServiceDescription:(nonnull MCDAppServiceDescription*) appServiceDescription;`

Initializes the [MCDAppServiceConnection](MCDAppServiceConnection.md) with app service details. The class instance will not request a connection until **openRemoteAsync** is called.

#### Returns
The initialized [MCDAppServiceConnection](MCDAppServiceConnection.md) if successful, otherwise nil.

### appServiceConnectionWithAppServiceDescription
`+ (nullable instancetype)appServiceConnectionWithAppServiceDescription:(nonnull MCDAppServiceDescription*) appServiceDescription;`

#### Parameters
* `appServiceDescription` The app service description.

#### Returns
The initialized [MCDAppServiceConnection](MCDAppServiceConnection.md) if successful, otherwise nil.

## Methods

### openRemoteAsync
`- (void)openRemoteAsync:(nonnull MCDRemoteSystemConnectionRequest*)connectionRequest completion:(nonnull void (^)(MCDAppServiceConnectionStatus, NSError* _Nullable))completion;`

Opens the app service connection on the specified remote device or application. If the connection fails to open, an exception is thrown.

#### Parameters
* `connectionRequest` The connection request indicating which remote app service to target.

### sendMessageAsync
`- (void)sendMessageAsync:(nonnull NSDictionary*)message completion:(nonnull void (^)(MCDAppServiceResponse* _Nonnull, NSError* _Nullable))completion;`

Sends a message to the remote app service and begins listening for a response. This method should only be called after the connection was opened successfully.

#### Parameters
* `message` The key-value set of data to be sent to the app service.

### close
`- (void)close;`

Closes the connection to the remote app service. The client app should call this method whenever it is closed or stopped by the user or system.

### addRequestReceivedListener
`- (NSUInteger)addRequestReceivedListener:(nonnull void (^)(MCDAppServiceConnection* _Nonnull, MCDAppServiceRequestReceivedEventArgs* _Nonnull))listener;`

Adds a request received event listener.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration token, a unique ID for this event listener.

### removeRequestReceivedListener
`- (void)removeRequestReceivedListener:(NSUInteger)eventRegistrationToken;`

Removes a request received event listener.

#### Parameters
* `eventRegistrationToken` The ID token for the event listener to remove.

### addServiceClosedListener
`- (NSUInteger)addServiceClosedListener:(nonnull void (^)(MCDAppServiceConnection* _Nonnull, MCDAppServiceClosedStatus))listener;`

Adds a service closed event listener.

#### Parameters
* `listener` The event listener. This must be implemented by the developer.

#### Returns
The event registration token, a unique ID for this event listener.

### removeServiceClosedListener
`- (void)removeServiceClosedListener:(NSUInteger)eventRegistrationToken;`

Removes a service closed event listener.

#### Parameters
* `eventRegistrationToken` The ID token for the event listener to remove.

### sendSingleMessageAsync
`+ (void)sendSingleMessageAsync:(nonnull NSDictionary*)message withConnection:(nonnull MCDRemoteSystemConnectionRequest*)connectionRequest appServiceDescription:(nonnull MCDAppServiceDescription*)appServiceDescription completion:(nonnull void (^)(MCDAppServiceResponse* _Nonnull, NSError* _Nullable))completion;`

Sends a message to a specified remote app service and begins listening for a response.

#### Parameters
* `message` The key-value set of data to be sent to the app service.
* `connectionRequest` The connection request specifying the app service to connect to.
* `appServiceDescription` The descriptive info for the target app service.

## Example
The following sample code uses an MCDAppServiceConnection and related classes to connect to a remote app service and exchange a simple message to compare date information and get the total delivery time.

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
