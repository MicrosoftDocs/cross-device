---
title: MCDRemoteSystemAccountFilter
description: Filter for the accounts to discover remote systems with.
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
A new instance of this class filter with the Account.

### initWithAccount
- (nullable instancetype)initWithAccount:(nonnull MCDConnectedDevicesAccount*)account;

Initialize the class with the MCDConnectedDevicesAccount account.

#### Parameters 
* `account` 

The MCDConnectedDevicesAccount account being used.

#### Returns
A new instance of this class filter with the Account.