---
description: Othent JS SDK getActiveAddress() function
---

# Get Active Address

Returns the Arweave wallet address associated with the active (authenticated) user account.

The wallet address is derived from the corresponding public key (see [`getActivePublicKey()`](get-active-public-key.md)).

```
getActiveAddress(): Promise<B64UrlString | "">;
```

**Returns:** A Promise with the wallet address (base64 `string`) of the active users, or an empty `string` if the user
is not authenticated.

{% hint style="info" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## Example usage

```ts
// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's wallet address:
const address = await othent.getActiveAddress();

console.log(`Your wallet address is ${ address }.`);
```
