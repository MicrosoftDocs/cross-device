---
title: MCDConnectedDevicesAccount
description: TODO
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDConnectedDevicesAccount`

```
@interface MCDConnectedDevicesAccount : NSObject
```  

MCDConnectedDevicesAccount is the result of a successful user sign in.

## Properties

### anonymousAccount
`+ (nullable instancetype)anonymousAccount;`

TODO

### accountId
`@property(nonatomic, readonly, copy, nonnull) NSString* accountId;`

TODO

### type
`@property(nonatomic, readonly) MCDConnectedDevicesAccountType type;`

TODO

## Constructors

### accountWithAccountId
`+ (nullable instancetype)accountWithAccountId:(nullable NSString*)accountId type:(MCDConnectedDevicesAccountType)type;`

TODO

#### Parameters 
* `type` TODO

#### Returns
TODO

### initWithAccountId
`- (nullable instancetype)initWithAccountId:(nullable NSString*)accountId type:(MCDConnectedDevicesAccountType)type;`

TODO

#### Parameters 
* `type` TODO

#### Returns
TODO