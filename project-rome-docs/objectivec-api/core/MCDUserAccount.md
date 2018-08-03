---
title: MCDUserAccount
description: This class represents a signed-in user.
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserAccount`

```
@interface MCDUserAccount : NSObject 
```

This class represents a signed-in user.

## Properties

### accountId
`@property(nonatomic, readonly, copy, nonnull) NSString* accountId;`

The unique identifier string for this user account.

### type
`@property(nonatomic, readonly) MCDUserAccountType type;`

The type of account.

## Constructors

### accountWithAccountId
`+ (nullable instancetype)accountWithAccountId:(nullable NSString*)accountId type:(MCDUserAccountType)type;`

#### Parameters
* `accountId` The unique identifier string for this user account.
* `type` The type of account.

#### Returns
A new instance of this class.

### initWithAccountId
`- (nullable instancetype)initWithAccountId:(nullable NSString*)accountId type:(MCDUserAccountType)type;`

#### Parameters
* `accountId` The unique identifier string for this user account.
* `type` The type of account.

#### Returns
A new instance of this class.

## Example
The following sample code shows how to register, retrieve, and delete a new user account

```ObjectiveC
NSString* _accountId;

// ...

- (void)_addAccount:(NSString*)refreshToken
{
    @synchronized(self)
    {
        NSLog(@"Add a account with id");
        // use a unique ID string for account ID
        _accountId = [[NSUUID UUID] UUIDString];

        // here it recommended to cache the refresh token
        // and raise the MCDUserAccountChangedEvent event.
    }
}

- (NSArray<MCDUserAccount*>*)getUserAccounts
{
    @synchronized(self)
    {
        // return a user account with the saved ID, if it exists.
        return (_accountId.length > 0) ? @[ [[MCDUserAccount alloc] initWithAccountId:_accountId type:MCDUserAccountTypeMSA] ] : nil;
    }
}

- (void)_removeAccount
{
    @synchronized(self)
    {
        NSLog(@"Remove the account");

        // clean account states (the app should have some mechanism of
        // determining when a user is signed in)
        if (_signedIn)
        {
            NSLog(@"Remove the account - clean cached account state");

            _signedIn = NO;
            _accountId = nil;
            // here it recommended to clear the cached refresh token
            // and raise the MCDUserAccountChangedEvent event.
        }
    }
}
```