---
description: Othent JS SDK sign() function
---

# Sign Transaction

To submit a transaction to the Arweave Network, it first has to be signed using a private key. The `sign()` function is meant to replicate the behavior of the `transactions.sign()` function of [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction), but instead of mutating the transaction object, it returns a new and signed transaction instance.

| Argument      | Type                                                                                                                     | Description                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| `transaction` | [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions)                                                  | A valid Arweave transaction instance (**without a keyfile**) |


{% hint style="warning" %}
**Tip:** A better alternative to this function is using the [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) `transactions.sign()` instead. Just omit the second parameter (`JWK` key) when calling the method, and [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) will automatically use ArConnect.
{% endhint %}

{% hint style="warning" %}
**Note:** If you are trying to sign a larger piece of data (5 MB <), make sure to notify the user to not switch / close the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.
{% endhint %}

## Example usage

### With `arweave-js` (recommended)

```ts
import Arweave from "arweave";

// create arweave client
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// create a transaction
const transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// sign using arweave-js
await arweave.transactions.sign(transaction);

// TODO: post the transaction to the network
```

### Directly using ArConnect

```ts
import Arweave from "arweave";

// create arweave client
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// create a transaction
let transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// sign using arweave-js
const signedFields = await window.arweaveWallet.sign(transaction);

// update transaction fields with the
// signed transaction's fields
transaction.setSignature({
  id: signedFields.id,
  owner: signedFields.owner,
  reward: signedFields.reward,
  tags: signedFields.tags,
  signature: signedFields.signature
});

// TODO: post the transaction to the network
```
