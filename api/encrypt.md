---
description: Othent JS SDK encrypt() function
---

# Encrypt

The `encrypt()` function encrypts the data using the active user's private key so that, when stored on Arweave, it is
only accessible to that specific user, similarly to the
[Web Crypto API's `encrypt()`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt). However, note
a current limitation of using _Othent_ is that the only available algorithm is RSA (`RSA-OAEP`).

This is useful for applications such as private file storage apps or mail/messaging platforms.

{% hint style="warning" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## API

```ts
encrypt(plaintext: string | BinaryDataType): Promise<Uint8Array>;
```

| Argument    | Type                                                                                                                                                                                                                                                                                                                                     | Description                                                                        |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `data`      | [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/ArrayBuffer), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/TypedArray) or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/DataView) | The data to be encrypted with the user's private key                               |

## Example usage

```typescript
// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Encrypt data using RSA:
const encrypted = await arweaveWallet.encrypt("This message will be encrypted");

console.log("Encrypted bytes:", encrypted);
```
