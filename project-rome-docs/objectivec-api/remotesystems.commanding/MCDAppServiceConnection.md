---
title: MCDAppServiceConnection
description:  This class manages a connection to a particular remote app service.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome 
---

# class `MCDAppServiceConnection`

```
@interface MCDAppServiceConnection : NSObject
```
This class manages a connection to a particular remote app service.

## Properties

### appServiceInfo
`@property(nonatomic, retain, nonnull) MCDAppServiceInfo* appServiceInfo;`

Provides details about the target app service to connect to.

### requestReceived 
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDAppServiceConnection*, MCDAppServiceRequestReceivedEventArgs*>* requestReceived;`

TODO

### serviceClosed 
`@property(nonatomic, readonly, nonnull) MCDEvent<MCDAppServiceConnection*, MCDAppServiceClosedEventArgs*>* serviceClosed;`

TODO

## Constructors

### init
`- (nullable instancetype)init;`

#### Returns
The initialized [MCDAppServiceConnection](MCDAppServiceConnection.md) if successful, otherwise nil.

### initWithAppServiceInfo
- (nullable instancetype)initWithAppServiceInfo:(nonnull MCDAppServiceInfo*) appServiceInfo;

#### Parameters
* `appServiceInfo` The app service description.

#### Returns
The initialized [MCDAppServiceConnection](MCDAppServiceConnection.md) if successful, otherwise nil.

### appServiceConnectionWithAppServiceInfo
`+ (nullable instancetype)appServiceConnectionWithAppServiceInfo:(nonnull MCDAppServiceInfo*) appServiceInfo;`

#### Parameters
* `appServiceInfo` The app service description.

#### Returns
The initialized [MCDAppServiceConnection](MCDAppServiceConnection.md) if successful, otherwise nil.

## Methods

### openRemoteAsync
`- (void)openRemoteAsync:(nonnull MCDRemoteSystemConnectionRequest*)connectionRequest completion:(nonnull void (^)(MCDAppServiceConnectionStatus, NSError* _Nullable))completion;`

Opens the app service connection on the specified remote device or application. If the connection fails to open, an exception is thrown.

>**Note:** This method will thrown an exception if any of the following are true:
> * The connection is already open or is in the process of opening.
> * The app service description has not been set or has been cleared.
> * The platform has not been initialized.
> * The app has subscribed a method to the connection's "request received" event but has not provided a **MCDNotificationProvider** when initializing the platform. All hosting scenarios require a **MCDNotificationProvider**.

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

### sendStatelessMessageAsync
```
+ (void)sendStatelessMessageAsync:(nonnull NSDictionary*)message
                     toAppService:(nonnull MCDAppServiceInfo*)appServiceInfo
                connectionRequest:(nonnull MCDRemoteSystemConnectionRequest*)connectionRequest
                       completion:(nonnull void (^)(MCDStatelessAppServiceResponse* _Nonnull, NSError* _Nullable))completion;
```

Sends a message to a specified remote app service and begins listening for a response.

#### Parameters
* `message` The key-value set of data to be sent to the app service.
* `appServiceInfo` The descriptive info for the target app service.
* `connectionRequest` The connection request specifying the app service to connect to.
* `completion` The connection request specifying the app service to connect to.