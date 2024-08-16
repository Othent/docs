---
description: Othent JS SDK walletName property
---

# Wallet Name

Indicates the name of the wallet, `"Othent KMS"` in this case.

## API

```ts
walletName: string;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

console.log(`Wallet Name = ${ Othent.walletName }`);

// or:

const othent = new Othent({ ... });

console.log(`Wallet Name = ${ othent.walletName }`);
```
