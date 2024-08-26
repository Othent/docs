---
description: Othent JS SDK config property
---

# Config

Configuration object used by the current `Othent` instance.

## API

```ts
config: OthentConfig;
```

### `OthentConfig`

`OthentConfig` is quite similar to [`OthentOptions`](./constructor.md#othentoptions) with some differences, as shown [here](./typescript-types.md#configtypes).

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

console.log("Current config =", othent.config);
```
