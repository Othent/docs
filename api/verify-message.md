---
description: Othent JS SDK verifyMessage() function
---

# Verify Message

The `verifyMessage()` function verifies a cryptographic signature created with the [`signMessage()`](sign-message.md),
either from Othent or from any other wallet such as ArConnect.

{% hint style="warning" %}
This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

{% hint style="info" %}
**Tip:** This function's implementation is compatible with ArConnect's `signMessage()` and `verifyMessage()`'s.
{% endhint %}

## API

```ts
verifyMessage(
  data: string | BinaryDataType,
  signature: string | BinaryDataType,
  publicKey?: B64UrlString,
  options: SignMessageOptions,
): Promise<boolean>;
```

### `data: string | BinaryDataType`

The data to verify the signature for.

### `signature: string | BinaryDataType`

The signature to validate.

### `publicKey?: B64UrlString`

The `publicKey` argument is optional. If it is not provided, the extension will use the currently authenticated user's
public key. You might only need this if the message to be verified was not made by the authenticated user. In that case,
this is the Arweave wallet `JWK.n` field or transaction owner field.

### `options: SignMessageOptions`

The `options` argument is optional. If it is not provided, the extension will use the `SHA-256` hash algorithm.

```ts
interface SignMessageOptions {
  hashAlgorithm?: "SHA-256" | "SHA-384" | "SHA-512";
}
```

### `return Promise<boolean>`

A `Promise` containing `true` if the signature was verified successfully, or `false` otherwise.

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

## Verification without Othent

You might encounter situations where you need to verify the signed message against an Othent generated signature, but
the SDK is not accessible or not installed (e.g.: third-party apps, server side code, unsupported browser....).

In these cases, it is possible to validate the signature by hashing the message (with the algorithm you used when
generating the signature using Othent) and verifying that against the Othent signature. This requires:

- The message to be verified.
- The signature.
- The algorithm used when the message was initially signed.
- The [wallet's public key](get-active-public-key.md).

Below is the JavaScript (TypeScript) example implementation with the
[Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web\_Crypto\_API), using `SHA-256` hashing:

```ts

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Message to be signed:
const data = "The hash of this msg will be signed.";

// Create signature:
const signature = await othent.signMessage(data);

// THIS IS WHERE WE START THE VERIFICATION:

// Hash the message (we used the default `signMessage()` options above, so Othent hashed the message using "SHA-256"):
const hash = await crypto.subtle.digest("SHA-256", data);

// Create JWK (JsonWebKey):
//
// We need the user's public key for this, that we'll get using `othent.getSyncActivePublicKey()` in this example, but
// in a real-world scenario that would have to come from somewhere else, such as:
//
// - Getting it from Othent (this example), ArConnect or any other wallet (if available).
// - Storing it beforehand.
// - If the wallet has made any transactions on the Arweave network
//   the public key is going to be the owner field of the mentioned
//   transactions.

const publicJWK: JsonWebKey = {
    e: "AQAB",
    ext: true,
    kty: "RSA",
    n: othent.getSyncActivePublicKey(),
};

// Import public JWK for verification:
const verificationKey = await crypto.subtle.importKey(
    "jwk",
    publicJWK,
    {
      name: "RSA-PSS",
      hash: "SHA-256"
    },
    false,
    ["verify"]
);

// Verify the signature by matching it with the hash:
const isValidSignature = await crypto.subtle.verify(
    { name: "RSA-PSS", saltLength: 32 },
    verificationKey,
    signature,
    hash
);

console.log(`The signature is ${isValidSignature ? "valid" : "invalid"}`);
```
