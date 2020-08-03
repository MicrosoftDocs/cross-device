---
title: MCDRemoteSystemKinds
description: Learn about the 'MCDRemoteSystemKinds' class. This class contains string fields that represent remote system device types.
keywords: microsoft, windows, iOS, iPhone, objectiveC, connected devices, Project Rome
---

# class `MCDRemoteSystemKinds` 

```
@interface MCDRemoteSystemKinds : NSObject
```

Contains string fields that represent remote system device types.

## Properties

### desktop
`@property(class, readonly, readonly, nonnull) NSString* desktop;`

The canonical name for the desktop device type.

### holographic
`@property(class, readonly, readonly, nonnull) NSString* holographic;`

The canonical name for the holographic device type.

### hub
`@property(class, readonly, readonly, nonnull) NSString* hub;`

The canonical name for the hub device type.

### phone
`@property(class, readonly, readonly, nonnull) NSString* phone;`

The canonical name for the phone device type.

### xbox
`@property(class, readonly, readonly, nonnull) NSString* xbox;`

The canonical name for the xbox device type.

### laptop
`@property(class, readonly, readonly, nonnull) NSString* laptop;`

The canonical name for the laptop device type.

> **Note:** All Microsoft Surface devices, including the Surface Book, are considered tablet devices.

### iot
`@property(class, readonly, readonly, nonnull) NSString* iot;`

The canonical name for the IoT device type.

### tablet
`@property(class, readonly, readonly, nonnull) NSString* tablet;`

The canonical name for the tablet device type.
