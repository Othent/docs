---
description: Othent custom events.
---

# Events

You can subscribe and unsubscribe to two different types of events from Othent (`auth` and `error`), using the
`addEventListener()` and `removeEventListener()` functions, respectively.

Additionally, `addEventListener()` returns a cleanup function that, when called, removes the event listener it created.

## `auth` Event:

```ts
const othent = new Othent({ throwErrors: false });

othent.addEventListener("auth", (userDetails: UserDetails | null, isAuthenticated: boolean) => {
  // If `userDetails != null` and `isAuthenticated = false`, this value comes from the cache.
});

othent.connect();
```

## `error` Event:

```ts
const othent = new Othent({ throwErrors: false });

othent.addEventListener("error", (err) => {
  // TODO: Handle error...
});

// This will throw an error:
othent.sign({ foo: "bar" } as unknown as Transaction);
```

Note that `error` type events are only fired when you set [`throwErrors = false`](./constructor.md).

See [Error Handling](#error-handling) above.