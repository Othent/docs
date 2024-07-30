---
description: Othent JS SDK privateHash() function
---

# Private Hash

The `privateHash()` function allows you to create deterministic secrets (hashes) from some data.

```
privateHash(
  data: string | BinaryDataType,
  options?: SignMessageOptions,
): Promise<Uint8Array>;
```

| Argument  | Type                                            | Description                |
| --------- | ----------------------------------------------- | -------------------------- |
| `data`    | `ArrayBuffer`                                   | The data to hash           |
| `options` | [`SignMessageOptions`](sign-message.md#options) | Configuration for the hash |

{% hint style="info" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

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
