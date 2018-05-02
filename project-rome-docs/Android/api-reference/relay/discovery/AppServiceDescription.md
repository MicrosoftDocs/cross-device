---
title: AppServiceDescription
description: This class describes an app service that belongs to a remote device or application.
keywords: microsoft, windows, device relay, Android, Android api reference 
---

# AppServiceDescription class 

```
public final class AppServiceDescription
```
This class describes an app service that belongs to a remote device or application.

## Constructors

### AppServiceDescription

`public AppServiceDescription(@NonNull String name, @NonNull String packageId)`

#### Parameters 
* `name` The name of the app service being described.
* `packageId` [optional] The package ID of the app service being described.

#### Returns
The initialized [AppServiceDescription](AppServiceDescription.md) if successful, otherwise `null`.

## Methods 

### getName
`public String getName()`

Gets the name of the app service.

#### Returns
A String of the app service name.

### getPackageId
`public String getPackageId()`

gets the package ID of the app service (equivalent to the package family name on Windows).

#### Returns
A String of the app service package ID.



