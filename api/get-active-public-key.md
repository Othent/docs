---
description: Othent JS SDK getActivePublicKey() function
---

# Get Active Public Key

Returns the public key (`jwk.n` field) associated with the active (authenticated) user account.

```
getActivePublicKey(): Promise<B64UrlString | "">;
```

**Returns:** A Promise with the owner (`jwk.n` field) (base64 `string`) of the active users, or an empty `string` if the
user is not authenticated.

{% hint style="info" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## Example usage

```ts
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
