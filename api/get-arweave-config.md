---
description: ArConnect Injected API getArweaveConfig() function
---

# Get Gateway Config

It can be useful to know what Arweave gateway the extension uses for your application.

You can set this when [instantiating Othent](./constructor.md#gatewayconfig-gatewayconfig) or when calling
[`connect()`](connect.md). 

## API

```ts
getArweaveConfig(): Promise<GatewayConfig>;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

const gatewayConfig = await othent.getArweaveConfig();

console.log("Current gateway config =", gatewayConfig);
```
