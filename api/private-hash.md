---
description: Othent JS SDK privateHash() function
---

# Private Hash

The `privateHash()` function allows you to create deterministic secrets (hashes) from some data.

{% hint style="warning" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## API

```ts
privateHash(
  data: string | BinaryDataType,
  options?: SignMessageOptions,
): Promise<Uint8Array>;
```

### `data: string | BinaryDataType`

The data to hash.

### `options?: SignMessageOptions`

The `options` argument is optional. If it is not provided, the extension will use the `SHA-256` hash algorithm.

```ts
interface SignMessageOptions {
  hashAlgorithm?: "SHA-256" | "SHA-384" | "SHA-512";
}
```

### `return Promise<Uint8Array>`

A `Promise` containing a `Uint8Array` with the hashed data.

## Example usage

```ts

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Data to be hashed:
const data = "The hash of this msg will be signed.";

// create the hash using the active wallet
const hash = await othent.privateHash(
    data,
    { hashAlgorithm: "SHA-256" }
);


console.log(`The hash is "${ hash }".`);
```
