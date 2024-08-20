---
description: Othent JS SDK signature() function
---

# Signature

{% hint style="danger" %}
**Deprecation warning:**

The `signature()` function is deprecated in Othent `2.0.0`, _ArConnect_ `1.0.0` and _Arweave.app_. Read about the
alternatives below:

There are quite a few cases where you might need to generate a cryptographic signature for a piece of data or message so
that you can verify them. The most common ones and their alternatives are the following:

- Generating a signature for a transaction: [`sign()`](sign.md)
- Generating a signature for a bundle data item: [`signDataItem()`](sign-dataitem.md) or [`dispatch()`](dispatch.md)
- Signing a message to later validate ownership: [`signMessage()`](sign-message.md) combined with [`verifyMessage()`](verify-message.md)

The safety of our users' wallets is our top priority, so we've decided to deprecate our `signature()` function,
following the example of _ArConnect_ and _Arweave.app_ and we expect other Arweave wallets now or in the future to do
the same. Eventually, this should be a smooth transition to the new alternatives. We are sorry for any inconveniences
caused by this change.

{% endhint %}

~~Often an application might need a piece of data that is created, authorized or confirmed by the owner of a wallet. The `signature()` function creates a cryptographical signature that allows applications to verify if a piece of data has been signed using a specific wallet. This function works similarly to the~~ [~~webcrypto sign API~~](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign)~~.~~

{% hint style="warning" %}
~~This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).~~
{% endhint %}

{% hint style="info" %}
~~**Tip:** Not to be confused with the [`sign()`](sign.md) function that is created to sign Arweave transactions.~~
{% endhint %}

## ~~API~~

```ts
signature(data: string | BinaryDataType): Promise<Uint8Array>;
```

### ~~`data: string | BinaryDataType`~~

~~The data to be signed with the user's private key.~~ 

### ~~`return Promise<Uint8Array>`~~

 ~~A `Promise` containing a `Uint8Array` with the signed data.~~ 

## ~~Example usage~~

```ts
// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Sign data:
const signature = await othent.signature("Data to sign");

console.log(`The signature is "${ signature }".`);
```
