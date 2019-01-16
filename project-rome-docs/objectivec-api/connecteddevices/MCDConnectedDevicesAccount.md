---
title: MCDConnectedDevicesAccount
description: This class represents a single user account known by an app.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesAccount`

```
@interface MCDConnectedDevicesAccount : NSObject
```  

This class represents a single user account known by an app.

## Properties

### anonymousAccount
`+ (nullable instancetype)anonymousAccount;`

The singleton instance of the Anonymous account.

### accountId
`@property(nonatomic, readonly, copy, nonnull) NSString* accountId;`

The unique identifier for this user account.

### type
`@property(nonatomic, readonly) MCDConnectedDevicesAccountType type;`

A MCDConnectedDevicesAccountType value describing the type of account.

## Constructors

### accountWithAccountId
`+ (nullable instancetype)accountWithAccountId:(nullable NSString*)accountId type:(MCDConnectedDevicesAccountType)type;`

A new instance of this class with the unique identifier for this user account.

#### Parameters 
* `type` 

The MCDConnectedDevicesAccountType of the account (depends on which ID provider the account is from).

#### Returns
Returns an MCDConnectedDevicesAccount object with the account identifier.

### initWithAccountId
`- (nullable instancetype)initWithAccountId:(nullable NSString*)accountId type:(MCDConnectedDevicesAccountType)type;`

A new instance of this class with the unique identifier for this user account.

#### Parameters 
* `type`

The MCDConnectedDevicesAccountType of the account (depends on which ID provider the account is from).

#### Returns
Returns an MCDConnectedDevicesAccount object initialized with the account identifier.