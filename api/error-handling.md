---
description: Othent error handling.
---

# Error Handling

All public `Othent` methods, except for the getters and properties, can throw an error when called under various
circumstances, so you should wrap them in `try-catch` blocks and handle errors appropriately.

{% hint style="warning" %}
Note throwing errors (`throwErrors: true`) is the default behavior unless you explicitly set `throwErrors: false`. Also
note that, for simplicity, all the examples in the docs use `throwErrors: false`.
{% endhint %}

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: true, ... });

// ...

const throwAnError = async () => {
  try {
    // Make sure the user is authenticated, or prompt them to authenticate:
    await othent.requireAuth();

    // This will throw an error:
    await othent.sign({ foo: "bar" } as unknown as Transaction);
  } catch (err) {
    // TODO: Handle error...
  }
}
```

## `throwErrors = false`

Alternatively, you can set [`throwErrors = false`](./constructor.md) to let `Othent` wrap all functions (except for
[`startTabSynching`](./start-tab-synching.md) and [`completeConnectionAfterRedirect`](./complete-connection-after-redirect.md))
in `try-catch` blocks automatically.

In this case, you must subscribe to `error` events using the `addEventListener()` function:

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false });

othent.addEventListener("error", (err) => {
  // TODO: Handle error...
});

// ...

const throwAnError = async () => {
  // Make sure the user is authenticated, or prompt them to authenticate:
  await othent.requireAuth();

  // This will throw an error:
  await othent.sign({ foo: "bar" } as unknown as Transaction);
}
```

## `OthentError`

`OthentError` is a custom JS/TS `class` extending `Error`.

{% hint style="warning" %}
TODO: We are still working on this. We'll update the documentation soon. Track the progress on this in this
[GitHub issue](https://github.com/Othent/KeyManagementService/issues/22).
{% endhint %}
