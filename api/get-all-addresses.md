---
description: Othent JS SDK getAllAddresses() function
---

# Get All Addresses

Returns an array of Arweave wallet addresses associated with the active (authenticated) user account.

```
getAllAddresses(): Promise<B64UrlString[]>;
```

**Returns:** A Promise with an array of all wallet addresses of the active user.

{% hint style="info" %}
**Note:** Othent does not currently support creating/storing more than one wallet associated to the same
account, so this function will always return exactly one wallet address.
{% endhint %}

{% hint style="info" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## Example usage

```ts
// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's wallet addresses:
const addresses = await othent.getAllAddresses();

console.log(`Your wallet addresses are ${ addresses.join(', ') }.`);
```
