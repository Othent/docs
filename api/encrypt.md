---
description: Othent JS SDK encrypt() function
---

# Encrypt

The `encrypt()` function encrypts the data using the active user's private key so that, when stored on Arweave, it is
only accessible to that specific user, similarly to the
[Web Crypto API's `encrypt()`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt).

This is useful for applications such as private file storage apps or mail/messaging platforms.

{% hint style="danger" %}
**Limitation:** There's currently an 8KB limit in data size when using Othent, but this is currently being worked on.
Track the progress on this [GitHub issue](https://github.com/Othent/KeyManagementService/issues/30).

**Limitation:** Also, the only currently available encryption/decryption algorithm is AES (`AES256-GCM`).
{% endhint %}

{% hint style="warning" %}
This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## API

```ts
encrypt(plaintext: string | BinaryDataType): Promise<Uint8Array>;
```

### `plaintext: string | BinaryDataType`

The data to be encrypted with the user's private key, which can be of type `string`, [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/ArrayBuffer), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/TypedArray) or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/DataView).

### `return Promise<Uint8Array>`

A `Promise` containing the encrypted data as [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array).

## Example usage

```typescript
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Encrypt data using RSA:
const encrypted = await othent.encrypt("This message will be encrypted");

console.log("Encrypted bytes:", encrypted);
```
