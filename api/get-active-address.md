---
description: Othent JS SDK getActiveAddress() function
---

# Get Active Address

Returns the Arweave wallet address associated with the active (authenticated) user account.

The wallet address is derived from the corresponding public key (see [`getActivePublicKey()`](get-active-public-key.md)).

## API

```ts
getActiveAddress(): Promise<B64UrlString | "">;
```

### `return Promise<B64UrlString | "">`

A `Promise` with the wallet address (Base64 URL-encoded `string`) of the active users, or an empty `string` if the user
is not authenticated.

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's wallet address:
const address = await othent.getActiveAddress();

console.log(`Your wallet address is ${ address }.`);
```
