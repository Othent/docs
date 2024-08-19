---
description: Othent JS SDK dispatch() function
---

# Dispatch Transaction

The `dispatch()` function allows you to quickly sign and send a transaction to the network in a bundled format. It is
best for smaller datas and contract interactions. If the bundled transaction cannot be submitted, it will fall back to a
base layer transaction. The function returns the [result](dispatch.md#dispatch-result) of the API call.

{% hint style="warning" %}
**Note:** This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).

**Note:** If you are trying to sign a larger piece of data (> 5 MB), make sure to notify the user to not switch / close
the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.

**Note:** The function uses the default bundler node, or the one passed as an option. Consider using the
[`signDataItem()`](sign-dataitem.md) function to create and sign a `DataItem` and manually send it to a custom bundler.
{% endhint %}

## API

```ts
dispatch(
  transaction: Transaction,
  options?: DispatchOptions,
): Promise<ArDriveBundledTransactionData | UploadedTransactionData>;
```

### `transaction: Transaction`

A valid Arweave [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions) instance, **without a keyfile**.

### `options?: DispatchOptions`

- #### `options?.node?: UrlString` (`string`)

  Node used for bundling transactions. Defaults to ArDrive Turbo's node.

- #### [`options?.arweave?: Arweave`](https://github.com/arweaveTeam/arweave-js#initialisation)

  Custom Arweave instance. Defaults to an instance connected to https://arweave.net:443.

### `return Promise<ArDriveBundledTransactionData | UploadedTransactionData>`

A `Promise` containing the result of the upload request, including the ID of the submitted transaction, as as well as a
`type` property indicating if it was uploaded by a bundle or directly to the base layer, as well as some additional
properties:

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
