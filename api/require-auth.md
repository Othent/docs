---
description: Othent JS SDK requireAuth() function
---

# Require Authentication

Checks if the user is authenticated and has a valid session. If they are not, they'll be prompted to authenticate, just
like [`connect()`](connect.md) does. However, this behavior depends on the `autoConnect` option used when instantiating
_Othent_:

- `autoConnect = "off"`: Calling `requireAuth()` will always throw an error if the user is not already authenticated.

  In this case, you should check [`isAuthenticated`](is-authenticated.md) yourself, and call [`connect()`](connect.md)
  if the user is not authenticated, before attempting to perform any operation with _Othent_.

- `autoConnect = "lazy"`: Authenticates them automatically, either from an existing session or by prompting them
  to sign in/up again. It throws an error if authentication fails.

- `autoConnect = "eager"`: Validates the user session or prompts the user to sign in/up again as soon as you instantiate
  _Othent_. 

  If the user is not authenticated, calling `requireAuth()` before the user interacts with the page (e.g. by clicking on
  a button), will throw a `Unable to open a popup` error.

  When using `auth0Strategy = "refresh-memory"` option (default), unless the user is already authenticated on the
  current tab, calling `requireAuth()` will throw a `Unable to open a popup` or `Missing Refresh Token` error.

{% hint style="warning" %}
All other functions (except the getters) call this function automatically to ensure they can perform the operation they
are supposed to, so unless you instantiated _Othent_ with `autoConnect = "off"`, you don't need to use it.
{% endhint %}

## API

```ts
requireAuth(): Promise<void>;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

// ...

const storeSecret = async (key: string, plaintext: string) => {
    // Make sure the user is authenticated, or prompt them to authenticate:
    await othent.requireAuth();

    // Now we can call other functions from Othent:
    const encryptedData = await othent.encrypt(plaintext);

    localStorage.set(key, encryptedData);
}
```
