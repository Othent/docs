---
description: Othent JS SDK decrypt() function
---

# Decrypt

The `decrypt()` function allows applications to decrypt data that has been encrypted using the active user's private
key, similarly to the [Web Crypto API's `decrypt()`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt).
However, note a current limitation of using _Othent_ is that the only available algorithm is RSA (`RSA-OAEP`).

{% hint style="warning" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## API

```ts
decrypt(ciphertext: BinaryDataType): Promise<string>;
```

### `ciphertext: BinaryDataType`

The data to be decrypted with the user's private key, which can be of type [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/ArrayBuffer), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/TypedArray) or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/DataView).

### `return Promise<string>`

A `Promise` containing the decrypted data as `string`.

## Example usage

```typescript
// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Encrypt data using RSA:
const encrypted = await othent.encrypt("This message will be encrypted");

console.log("Encrypted bytes:", encrypted);

// Decrypt the same data using RSA:
const decrypted = await othent.decrypt(encrypted);

console.log(`The original secret message is "${ decrypted }".`);
```
