---
description: Othent JS SDK walletVersion property
---

# Wallet Name

Indicates what _Othent_ (`@othent/kms`) version you are using, following [semver](https://semver.org/).

## API

```ts
walletVersion: string;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

console.log(`Wallet Version = ${ Othent.walletVersion }`);

// or:

const othent = new Othent({ ... });

console.log(`Wallet Version = ${ othent.walletVersion }`);
```
