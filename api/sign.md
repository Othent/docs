---
description: Othent JS SDK sign() function
---

# Sign Transaction

To submit a transaction to the Arweave Network, it first has to be signed using a private key. Othent creates a private
key / Arweave wallet for every account and stores it in Google KMS. The wallet associated with the active user account
is used to sign transactions using the `sign()` function.

The `sign()` function is meant to replicate the behavior of the `transactions.sign()` function of
[`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction), but instead of mutating the transaction
object, it returns a new and signed transaction instance.

TODO: Implement this, as right now we actually mutate the same transaction.

TODO: Check if we can make Othent work like in the first hint.

```
sign(transaction: Transaction): Promise<Transaction>;
```

| Argument      | Type                                                                                                                     | Description                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| `transaction` | [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions)                                                  | A valid Arweave transaction instance (**without a keyfile**) |

**Returns:** A Promise containing the signed transaction.

{% hint style="warning" %}
**Tip:** A better alternative to this function is using the [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) `transactions.sign()` instead. Just omit the second parameter (`JWK` key) when calling the method, and [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) will automatically use ArConnect.
{% endhint %}

{% hint style="warning" %}
**Note:** If you are trying to sign a larger piece of data (5 MB <), make sure to notify the user to not switch / close the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.
{% endhint %}

{% hint style="info" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## Example usage

### With `arweave-js` (recommended)

```ts
import Arweave from "arweave";

// Create an Arweave client:
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Create a transaction:
const transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// Sign using arweave-js:
await arweave.transactions.sign(transaction);

// TODO: Post the `transaction` to the network...
```

### Directly using Othent

```ts
import Arweave from "arweave";

// Create an Arweave client:
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Create a transaction:
let transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// Sign using Othent:
const signedTransaction = await othent.sign(transaction);

// TODO: Post `signedTransaction` to the network...
```
