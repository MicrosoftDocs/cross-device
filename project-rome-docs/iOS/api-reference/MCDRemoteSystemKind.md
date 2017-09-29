---
title: MCDRemoteSystemKind
description:  Contains values that describe the status of a response message from a remote app service.
keywords: microsoft, windows, project rome, how-to iOS, how-to iPhone
---

# enum `MCDRemoteSystemKind` 

```
typedef NS_ENUM(NSInteger, MCDRemoteSystemKind)
```

Contains values that represent remote system device types.

## Fields

Name  | Value                                
--------------------------------|---------------------------------------------
MCDRemoteSystemKindUnknown | 0
MCDRemoteSystemKindDesktop | 1
MCDRemoteSystemKindHolographic | 2
MCDRemoteSystemKindPhone | 3
MCDRemoteSystemKindXbox | 4
MCDRemoteSystemKindHub | 5

## Methods

### MCDRemoteSystemFriendlyNameForKind
`NSString* MCDRemoteSystemFriendlyNameForKind(MCDRemoteSystemKind type);`

Returns a string representation for a remote system kind.

#### Parameters
* `type` - The device type.

#### Returns
The string representation for the given remote system kind.