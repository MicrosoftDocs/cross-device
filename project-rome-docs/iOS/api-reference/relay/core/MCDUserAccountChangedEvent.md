---
title: MCDUserAccountChangedEvent
description: An event indicating that a user account has been changed (added, removed, interrupted, fixed)
keywords: microsoft, windows, device relay, how-to iOS, how-to iPhone 
---

# class `MCDUserAccountChangedEvent`

```
 @interface MCDUserAccountChangedEvent : NSObject
 ```

An event indicating that a user account has been changed (added, removed, interrupted, fixed). It is listened to by the connected devices platform.

## Properties

### subscriberCount
`@property(atomic, readonly) NSUInteger subscriberCount;`

The current number of listeners for this event.

## Methods

### subscribe
`- (NSUInteger)subscribe : (nonnull void (^)())callback;`

Subscribes to this event, receiving a callback whenever the event is raised

#### Parameters
* `callback` The callback method to be registered to this event.

#### Returns
An integer identifying the event registration

### unsubscribe
`- (void)unsubscribe:(NSUInteger)registration;`

Unsubscribes from this event, using the event registration ID.

#### Parameters
* `registration` The event registration ID.

### raise
`- (void)raise;`

Raises this event, informing all listeners from the connected devices framework that a user account has changed.

### setRegistrationCallback
`- (void)setRegistrationCallback:(nonnull void (^)(MCDEventRegistrationStatus))callback;`

Sets a callback method to be called whenever a new listener is registered to this event.

#### Parameters
* `callback` The callback method to set.

## Example
The following sample code shows how to register, retrieve, and delete a new user account

```Objective-C
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