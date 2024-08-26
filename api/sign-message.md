---
description: Othent JS SDK signMessage() function
---

# Sign Message

The `signMessage()` function creates a cryptographic signature of any data (after hashing it) for later validation,
using the active (authenticated) user's private key.

{% hint style="warning" %}
This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).

Also, this function should only be used to allow data validation. It cannot be used for on-chain transactions,
interactions or bundles, for security reasons. Consider using [`sign()`](sign.md),
[`signDataItem()`](sign-dataitem.md) or [dispatch()](dispatch.md) instead.
{% endhint %}

{% hint style="info" %}
**Tip:** This function's implementation is compatible with ArConnect's `signMessage()` and `verifyMessage()`'s.

**Tip**: The function first hashes the input data for security reasons. We recommend using the built in
[`verifyMessage()`](verify-message.md) function to validate the signature, or hashing the data the same way, before
validation ([example](verify-message.md#verification-without-arconnect)).
{% endhint %}

## API

```ts
signMessage(
  data: string | BinaryDataType,
  options?: SignMessageOptions,
): Promise<Uint8Array>;
```

### `data: string | BinaryDataType`

The data to generate the signature for.

### `options?: SignMessageOptions`

The `options` argument is optional. If it is not provided, the extension will use the `SHA-256` hash algorithm.

```ts
interface SignMessageOptions {
  hashAlgorithm?: "SHA-256" | "SHA-384" | "SHA-512";
}
```

### `return Promise<Uint8Array>`

A `Promise` containing an `Uint8Array` with the signed hash of the data, which can be verified with
[`Othent.verifyMessage`](./verify-message.md).

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Message to be signed:
const data = "The hash of this msg will be signed.";

// Create signature:
const signature = await othent.signMessage(data);

// Verify signature:
const isValidSignature = await othent.verifyMessage(data, signature);

console.log(`The signature is ${isValidSignature ? "valid" : "invalid"}`);
```
