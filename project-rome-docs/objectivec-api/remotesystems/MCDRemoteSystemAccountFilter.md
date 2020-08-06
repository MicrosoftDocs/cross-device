---
title: MCDRemoteSystemAccountFilter
description: "Learn how to filter for accounts to discover remote systems by using constructors like 'filterwithAccount'."
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemAccountFilter` 

```
@interface MCDRemoteSystemAccountFilter : NSObject<MCDRemoteSystemFilter>
```  

Filter for the accounts to discover remote systems with.

## Properties

### account
`@property(nonatomic, readonly, strong, nonnull) MCDConnectedDevicesAccount* account;`

The Account associated with this MCDRemoteSystemAccountFilter.

## Constructors

### filterWithAccount
`+ (nullable instancetype)filterWithAccount:(nonnull MCDConnectedDevicesAccount*)account;`

Initialize the class with the MCDConnectedDevicesAccount account.

#### Parameters 
* `account` 

The MCDConnectedDevicesAccount account being used.

#### Returns
Returns a MCDRemoteSystemAccountFilter object filtered with the Account.

### initWithAccount
`- (nullable instancetype)initWithAccount:(nonnull MCDConnectedDevicesAccount*)account;`

Initialize the class with the MCDConnectedDevicesAccount account.

#### Parameters 
* `account` 

The MCDConnectedDevicesAccount account being used.

#### Returns
Returns an MCDRemoteSystemAccountFilter object initialized filtered with the Account.