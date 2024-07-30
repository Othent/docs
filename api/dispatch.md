---
description: Othent JS SDK dispatch() function
---

# Dispatch Transaction

The `dispatch()` function allows you to quickly sign and send a transaction to the network in a bundled format. It is
best for smaller datas and contract interactions. If the bundled transaction cannot be submitted, it will fall back to a
base layer transaction. The function returns the [result](dispatch.md#dispatch-result) of the API call.

```
dispatch(
  transaction: Transaction,
  options?: DispatchOptions,
): Promise<ArDriveBundledTransactionData | UploadedTransactionData>;
```

| Argument      | Type                                                                    | Description                                                  |
| ------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------ |
| `transaction` | [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions) | A valid Arweave transaction instance (**without a keyfile**) |
| `options?.node?` | `UrlString` (`string`) | Node used for bundling transactions. Defaults to ArDrive Turbo's node. |
| `options?.arweave?` | [`Arweave`](https://github.com/arweaveTeam/arweave-js#initialisation) | Custom Arweave instance. Defaults to an instance connected to http://arweave.net:443. |

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

The `dispatch()` function returns the result of the operation, including the ID of the submitted transaction, as well as
if it was submitted in a bundle or on the base layer.

```ts
interface ArDriveBundledTransactionData {
  type: "BUNDLED";
  id: string;
  timestamp: number;
  winc: string;
  version: string;
  deadlineHeight: number;
  dataCaches: string[];
  fastFinalityIndexes: string[];
  public: string;
  signature: string;
  owner: string;
}

interface UploadedTransactionData {
  type: "BASE";
  id: string;
  signature: string;
  owner: string;
}
```

## Example usage

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

// Dispatch (and sign) it using the default bundler:
const dispatchResult = await othent.dispatch(transaction);

console.log(`The transaction was dispatched as a ${ dispatchResult.type === "BUNDLED" ? "bundled" : "base layer" } Arweave transaction.`);
```
