---
description: Othent JS SDK signMessage() function
---

# Sign Message

The `signMessage()` function creates a cryptographic signature of any data (after hashing it) for later validation,
using the active (authenticated) user's private key.

{% hint style="warning" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).

**Note**: This function should only be used to allow data validation. It cannot be used for on-chain transactions,
interactions or bundles, for security reasons. Consider implementing [`sign()`](sign.md),
[`signDataItem()`](sign-dataitem.md) or [dispatch()](dispatch.md).

**Note**: The function first hashes the input data for security reasons. We recommend using the built in
[`verifyMessage()`](verify-message.md) function to validate the signature, or hashing the data the same way, before
validation ([example](verify-message.md#verification-without-arconnect)).
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature
options (default hash algorithm: `SHA-256`) to sign the data.

**Note:** This function's implementation is compatible with ArConnect's `signMessage()` and `verifyMessage()`'s.
{% endhint %}

## API

```ts
signMessage(
  data: string | BinaryDataType,
  options?: SignMessageOptions,
): Promise<Uint8Array>;
```

| Argument   | Type                                            | Description                            |
| ---------- | ----------------------------------------------- | -------------------------------------- |
| `data`     | `ArrayBuffer`                                   | The data to generate the signature for |
| `options?` | [`SignMessageOptions`](sign-message.md#options) | Configuration for the signature        |

## Options

Currently ArConnect allows you to customize the hash algorithm (`SHA-256` by default):

```typescript
export interface SignMessageOptions {
  hashAlgorithm?: "SHA-256" | "SHA-384" | "SHA-512";
}
```

## Example usage

```ts

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
