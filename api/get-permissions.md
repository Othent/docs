---
description: ArConnect Injected API getPermissions() function
---

# Get Permissions

As discussed in [`connect()`'s Permissions section](connect.md#permissions), users using _Othent_ are implicitly giving
dApps that use _Othent_ full control of their wallets. 

Therefor, the `getPermissions()` function always returns an array with all possible permissions.

## API

```ts
getPermissions(): Promise<PermissionType[]>;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

const permissions = await othent.getPermissions();

console.log(`Othent has the following permissions = ${ permissions.join(", ") }`);
```
