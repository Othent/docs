---
description: Othent JS SDK getWalletNames() function
---

# Get Wallet Names

Similarly to ArConnect, each wallet in Othent has a nickname. This is either:

- The user's [ANS](https://ans.gg) name. TODO: To be implemented...
- A platform + email identifying label (e.g. `Google (email@gmail.com)`, `Twitter (email@outlook.com)`...).

To provide better UX, you can retrieve these names from the active (authenticated) user account and display them to make 
it easier for the user to recognize which wallet they're using. 

{% hint style="info" %}
Othent does not currently support creating/storing more than one wallet associated to the same account, so this function
will always return exactly one wallet address.
{% endhint %}

## API

```ts
getWalletNames(): Promise<Record<B64UrlString, string>>;
```

### `return Promise<Record<B64UrlString, string>>`

A `Promise` containing an object that maps each wallet addresses of the active user to their nickname, or an empty
`Object` if the user is not authenticated.

## Example usage

```ts
// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's wallet names from:
const walletNames = await othent.getWalletNames();

// Obtain the user's active wallet address:
const activeAddress = await othent.getActiveAddress();

console.log(`Your active wallet's nickname is ${ walletNames[activeAddress] }.`);
```
