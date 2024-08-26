---
description: Othent custom events.
---

# Events

You can subscribe and unsubscribe to two different types of events from Othent (`auth` and `error`), using the
`addEventListener()` and `removeEventListener()` functions, respectively.

Additionally, `addEventListener()` returns a cleanup function that, when called, removes the event listener it created.

## `auth` Event:

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

othent.addEventListener("auth", (userDetails: UserDetails | null, isAuthenticated: boolean) => {
  // If `userDetails != null` and `isAuthenticated = false`, this value comes from the cache.
});

await othent.connect();
```

{% hint style="warning" %}
The value you get when calling `getUserDetails()` or when subscribing to the `auth` event before authenticating by
calling `connect()` or `requireAuth()` (either manually or automatically by setting `autoConnect = "eager"`), will be
(in this order of priority):

- The value you pass as `initialUserDetails`, if any. 
- The value stored in `localStorage`, if you set `persistLocalStorage`.
- `null` otherwise.

`@othent/kms` does not performs any type of validation when reading the user details from these sources, and therefore
you should treat that data as untrusted and make sure you sanitize it appropriately.

Failing to do that could result in your application being vulnerable to XSS if an attacker manages to tamper with these
values.
{% endhint %}

## `error` Event:

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

Note that `error` type events are only fired when you set [`throwErrors = false`](./constructor.md).

See [Error Handling](#error-handling).