---
description: Othent error handling.
---

# Error Handling

All public `Othent` methods, except for the getters and properties, can throw an error when called under various
circumstances, so you should wrap them in `try-catch` blocks and handle errors appropriately.

Alternatively, you can set [`throwErrors = false`](./constructor.md) to let `Othent` wrap all functions in `try-catch`
blocks automatically. In this case, you must subscribe to `error` events using the `addEventListener()` function:

```ts
const othent = new Othent({ throwErrors: false });

othent.addEventListener("error", (err) => {
  // TODO: Handle error...
});

// This will throw an error:
othent.sign({ foo: "bar" } as unknown as Transaction);
```

> TODO: Document custom error class and error types.