---
description: Othent JS SDK dispatch() function
---

# Dispatch Transaction

The `dispatch()` function allows you to quickly sign and send a transaction to the network in a bundled format. It is
best for smaller datas and contract interactions. If the bundled transaction cannot be submitted, it will fall back to a
base layer transaction. The function returns the [result](dispatch.md#dispatch-result) of the API call.

The `dispatch()` function supports the following arguments:

- **Arweave transaction**: A valid Arweave transaction object is required.
- **Optional Parameters**:
    - **Bundling Node:** Specify the node used for bundling transactions. By default, the function uses the ArDrive Turbo node.
    - **Arweave Init Instance:** Provide a custom Arweave initialization instance By default, the function uses an arweave instance connected to [`arweave.net`](http://arweave.net) on port `443`.

| Argument      | Type                                                                    | Description                                                  |
| ------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------ |
| `transaction` | [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions) | A valid Arweave transaction instance (**without a keyfile**) |

{% hint style="warning" %}
**Note:** If you are trying to sign a larger piece of data (5 MB <), make sure to notify the user to not switch / close the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.
{% endhint %}

{% hint style="warning" %}
**Note:** The function uses the default bundler node set by the user or the extension. Consider using the [`signDataItem()`](sign-dataitem.md) function to submit data to a custom bundler.
{% endhint %}

{% hint style="info" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

## Dispatch result

The `dispatch()` function returns the result of the operation, including the ID of the submitted transaction, as well as if it was submitted in a bundle or on the base layer.

```ts
export interface DispatchResult {
  id: string;
  type?: "BASE" | "BUNDLED";
}
```

## Example usage

```ts
import Arweave from "arweave";

// create arweave client
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// connect to the extension
await window.arweaveWallet.connect(["DISPATCH"]);

// create a transaction
const transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// dispatch the tx
const res = await window.arweaveWallet.dispatch(transaction);

console.log(`The transaction was dispatched as a ${res.type === "BUNDLED" ? "bundled" : "base layer"} Arweave transaction.`)
```