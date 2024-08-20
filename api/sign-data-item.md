---
description: Othent JS SDK signDataItem() function
---

# Sign Data Item

The `signDataItem()` function allows you to create and sign a `DataItem` object, compatible with
[`arbundles`](https://npmjs.com/arbundles). These data items can then be submitted to an
[ANS-104](https://github.com/ArweaveTeam/arweave-standards/blob/master/ans/ANS-104.md) compatible bundler.

{% hint style="warning" %}
This function assumes (and requires) a user is authenticated. See [`requireAuth()`](require-auth.md).
{% endhint %}

{% hint style="info" %}
**Tip:** The function returns a buffer (`ArrayBufferLike`) of the signed data item. You'll need to manually load it
into an [`arbundles`](https://npmjs.com/arbundles) `DataItem` instance as seen in the
[example usage](sign-dataitem.md#example-usage):
{% endhint %}

## API

```ts
signDataItem(dataItem: DataItem): Promise<ArrayBufferLike>;
```

### `dataItem: DataItem`

The bundled data item's data (not [`arbundle`'s `DateItem` instance](https://github.com/Irys-xyz/arbundles)) to sign.

```ts
interface DataItem {
    data: string | Uint8Array;
    target?: string;
    anchor?: string;
    tags?: {
        name: string;
        value: string;
    }[];
}
```

### `return Promise<ArrayBufferLike>`

A `Promise` containing an `ArrayBuffer` with the `DataItem`'s signed data, which can be loaded into a [`arbundle`'s `DateItem` instance](https://github.com/Irys-xyz/arbundles) for validation.

## Example usage

```ts
import { DataItem } from "arbundles";
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Sign the DataItem:
const signedDataItemBuffer = await othent.signDataItem({
    data: "This is an example data",
    tags: [{
        name: "Content-Type",
        value: "text/plain"
    }]
});

// Load the result into a DataItem instance:
const dataItem = new DataItem(signedDataItemBuffer);

// Verify the DataItem's signature:
const isValid = await dataItem.isValid();

if (isValid) {
    // Submit it to a bundler:
    await fetch(`https://node2.bundlr.network/tx`, {
        method: "POST",
        headers: {
            "Content-Type": "application/octet-stream"
        },
        body: dataItem.getRaw()
    });
}
```
