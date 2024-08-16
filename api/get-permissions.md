---
description: ArConnect Injected API getPermissions() function
---

# Get Permissions

As discussed in [`connect()`'s Permissions section](connect.md#permissions), _Othent_ being a custodial wallet, it
implicitly requires all permission. Therefor, the `getPermissions()` function returns an array with all possible
permissions.

## API

```ts
getPermissions(): Promise<PermissionType[]>;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

const permissions = await othent.getPermissions();

console.log(`Othent has the following permissions = ${ permissions.join(", ") }`);
```
