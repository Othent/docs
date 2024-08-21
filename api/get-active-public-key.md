---
description: Othent JS SDK getActivePublicKey() function
---

# Get Active Public Key

Returns the public key (`jwk.n` field) associated with the active (authenticated) user account.

## API

```ts
getActivePublicKey(): Promise<B64UrlString | "">;
```

### `return Promise<B64UrlString | "">`

A `Promise` with the owner public key (`jwk.n` field, as a Base64 URL-encoded `string`) of the active (authenticated)
user, or an empty `string` if the user is not authenticated.

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's active wallet address:
const publicKey = await othent.getActivePublicKey();

console.log(`JWK.n field is ${ publicKey }.`);

// Create public key JWK:
const publicJWK: JsonWebKey = {
    e: "AQAB",
    ext: true,
    kty: "RSA",
    n: publicKey
};

// Import it with WebCrypto, etc.
```
