---
description: Othent JS SDK sign() function
---

# Sign Transaction

The `sign()` function signs an Arweave [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions) using the
current user's private key. It's meant to replicate the behavior of the `transactions.sign()` function of
[`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction), but instead of mutating the transaction
object, it returns a new and signed transaction instance.

{% hint style="warning" %}
**Tip:** A better alternative to this function is using the
[`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) `transactions.sign()` instead. Just omit
the second parameter (`JWK` key) when calling the method, and
[`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) will automatically use `Othent` (if it was
instantiated with `inject = true`).

See [Indirect Usage (through `arweave-js`)](./intro.md#indirect-usage-through-arweave-js)

**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).

**Note:** If you are trying to sign a larger piece of data (> 5 MB), make sure to notify the user to not switch / close
the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.
{% endhint %}

## API

```ts
sign(transaction: Transaction): Promise<Transaction>;
```

### `transaction: Transaction`

A valid Arweave [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions) instance, **without a keyfile**.

### `return Promise<Transaction>`

A `Promise` containing a new signed [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions) instance.

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

// Sign it using arweave-js:
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

// Sign it using Othent:
const signedTransaction = await othent.sign(transaction);

// TODO: Post `signedTransaction` to the network...
```
