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

`OthentConfig` is quite similar to [`OthentOptions`](./constructor.md#othentoptions) with some differences.

{% hint style="info" %}
Take a look at the [TypeScript `OthentOptions` and `OthentConfig` interfaces on GitHub](https://github.com/Othent/KeyManagementService/blob/main/src/lib/config/config.types.ts)
for additional details.
{% endhint %}

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

console.log("Current config =", othent.config);
```
