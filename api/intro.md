---
description: https://github.com/Othent/package
---

# 🥪 Othent JS SDK

The Othent JS SDK is a `class` (`Othent`) that exposes a collection of functions that enable interaction with wallet
under Othent's custody. These functions are designed to make it seamless for developers to integrate Othent into their
applications, and closely follow [`ArConnect`'s API](https://docs.arconnect.io/) to provide a familiar interface.

## Installation & Setup

To use the library in your project, you can install it using `npm` / `pnpm` / `yarn`:

```bash
npm i othent
pnpm i othent
yarn i othent
```

To use Othent in production, you'll also need to reach out to the [Othent team on Discord](https://discord.gg/gWDmJep5)
to get your domain whitelisted.

Lastly, simply instantiate `Othent` with any options you need.

Additionally, if you set the `persistLocalStorage` option to persist and sync user details across tabs, you need to call
`startTabSynching` and make sure the cleanup function it returns is called once you no longer need the `Othent` instance
you've created.

Here's an example inside a React component:

```ts
const MyComponent = () => {
  const othent = useMemo(() => {
    return new Othent(options);
  }, [options]);

  useEffect(() => {
      const cleanupFn = othent.init();

      return () => {
        cleanupFn();
      };
  }, [othent])
}
```

If you are using Othent with React, you might want to consider using
[React's Context](https://react.dev/learn/passing-data-deeply-with-context) to use a single `Othent` instance for your
whole app, or decoupling it even more by using a state management library like [MobX](https://mobx.js.org/README.html),
[TanStack Query](https://tanstack.com/query/latest) or [Redux](https://redux.js.org/). 

### React Native

Othent directly uses the [Web/Node.js Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Crypto) to create
hashes, verify signatures and, indirectly, through [`arweave-js`](https://github.com/ArweaveTeam/arweave-js). If your
environment doesn't has this API natively, you'll have to polyfill it.

Next, update your platform-specific configuration files to work with Auth0:

- See ["Integrate Auth0 in Your Application"](https://auth0.com/docs/quickstart/native/react-native/00-login#integrate-auth0-in-your-application)
  to update your `build.gradle` and `AppDelegate.mm` files. Othent's Auth0 domain is `auth.othent.io`.

- See ["Configure Callback and Logout URLs"](https://auth0.com/docs/quickstart/native/react-native/00-login#configure-callback-and-logout-urls)
  to define your callback and logout URLs.
  
Then, you need to set (at least) the following options when instantiating `Othent`:

- `auth0LogInMethod = "redirect"`
- `auth0RedirectURI`: Based on the values defined above.
- `auth0ReturnToURI`: Based on the values defined above.
- `auth0Cache`: You have to pass a custom [`ICache`](https://auth0.github.io/auth0-spa-js/interfaces/ICache.html)
  implementation. This object will be responsible of persisting the refresh tokens, so, on iOS, we recommend
  implementing it using [Keychain Services](https://developer.apple.com/documentation/security/keychain_services/).

Lastly, make sure when Auth0 redirects the user back to your app (`auth0RedirectURI`), you call
`completeConnectionAfterRedirect`, passing the URI with the `code` and `state` params provided by Auth0, which handles 
the redirect callback. See [`handleRedirectCallback`](https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#handleRedirectCallback).

## Indirect Usage (through `arweave-js`)

Similarly to using ArConnect or other browser-based wallets, to use Othent in your application, you don't need to
integrate or learn how the Othent JS SDK API works. Using [`arweave-js`](https://npmjs.com/arweave), you can easily sign
transactions through Othent.

To use Othent library like this:

  1. Import it into your project.
  2. Instantiate it passing in the `inject = true` option. This will set `window.arweaveWallet` to this `Othent`
     instance.
  3. Now you can use [`arweave-js`](https://npmjs.com/arweave), which will use Othent in the background.

```ts
import { Othent } from "@othent/kms";

new Othent({ inject: true, ... });

// Create an Arweave transaction:
const tx = await arweave.createTransaction({ /* Transaction options */ });

// Sign the transaction:
await arweave.transactions.sign(tx);

// Do something else with the transaction (e.g. post it to the network).
```

When signing a transaction through [`arweave-js`](https://npmjs.com/arweave), you'll need to omit the second argument of
the `sign()` function, or set it to `"use_wallet"`. This will let the package know you want to use the injected wallet,
which has been exposed at `window.arweaveWallet`, to sign the transaction in the background.

Once the transaction is signed, you can safely post it to the network.

## Indirect Usage (through Arweave Wallet Kit)

We are still working on this. We'll update the documentation soon.

TODO: Implement AWK strategy.

## Direct Usage (through `Othent` instance)

Alternatively, you can also use Othent's JS SDK directly, which provides some extra functionalities. These features are
not integrated in the [`arweave-js`](https://npmjs.com/arweave) package, but can be useful to further customize your
app.

To use Othent library like this:

  1. Import it into your project.
  2. Instantiate it (no need for `inject = true` in this case).
  3. Now you can access Othent's properties & methods directly from the `Othent` instance. Each property & method is
  described in detail in the following pages.

See here for a basic example:

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

// [...]

await othent.connect();

const mySecret = await othent.encrypt("My secret");

const transaction = await arweave.createTransaction({
  data: imySecret,
});

await othent.dispatch(transaction);
```

## Additional Options

When instantiating `Othent`, you can use the following options (`OthentOptions`) to customize its behavior:

- `appName: string`:  Name of your app. This will add a tag `App-Name: <appName>` to any transaction signed or sent
  using `Othent.sign`, `Othent.dispatch` or `Othent.signDataItem`.

- `appVersion: string`: Version of your app. This will add a tag `App-Version: <appVersion>` to any transaction signed
  or sent using `Othent.sign`, `Othent.dispatch` or `Othent.signDataItem`.

- `persistCookie: boolean | OthentStorageKey`: Set this to `true` or the name of the cookie where you'd like the user
  details JSON to be stored.
  
  Note setting this option to `true` will set the cookie on the client / frontend, but it won't recover it on the
  server / backend. If you are using SSR, you need to use `cookie = true` in conjunction with `initialUserDetails`.
  
  Default: `false`

- `persistLocalStorage: boolean | OthentStorageKey`: Set this to `true` or the name of the `localStorage` item where
  you'd like the user details JSON to be stored.
  
  Note the stored values will be removed / discarded if more than `refreshTokenExpirationMs` have passed, but will
  remain in `localStorage` until then or until the user logs out.
  
  Default: `false`

- `gatewayConfig?: GatewayConfig`: Gateway config to connect to Arweave.

- `initialUserDetails?: UserDetails | null`: Initial user details. Useful for server-side rendered sites or native apps
  that might store the most recent user details externally (e.g. cookie or `SharedPreferences`).

- `debug: boolean`: Enable additional logs.

  Default: `false`

- `inject: boolean`: Inject Othent's instance as `window.arweaveWallet` so that `arweave-js` can use it on the
  background.

  Default: `false`

- `serverBaseURL: string`: API base URL. Needed if you are using a private/self-hosted API and Auth0 tenant.

- `auth0Domain: string`: Auth0 domain. Needed if you are using a private/self-hosted API and Auth0 tenant.

- `auth0ClientId: string`: Auth0 client ID. Needed if you are using a private/self-hosted API and Auth0 tenant, or if
  you have a dedicated App inside Othent's Auth0 tenant to personalize the logic experience (premium subscription).

- `auth0Strategy: Auth0Strategy`: Possible values are:
    
  - `memory`: This is the most secure and recommended option/location to store tokens, but new tabs won't be able to
    automatically log in using a popup without a previous user action.
  
    However, by setting the `persistLocalStorage = true` option, the user details (but not the refresh / access
    tokens) will be persisted in `localStorage` until the most recent refresh token's expiration date, allowing you
    to read the user details (`.getUserDetails()` / `.getSyncUserDetails()`) and make it look in the UI as if the
    user were already logged in.
  
  - `localstorage`: Store tokens `localStorage`. This makes it possible for new tabs to automatically log in using a
    popup, even after up to 2 weeks of inactivity (i.e. "keep me logged in"), but offers a larger attack surface to
    attackers trying to get a hold of the refresh / access tokens.
   
  - `custom`: Provide a custom storage implementation that implements Auth0's
    [`ICache`](https://auth0.github.io/auth0-spa-js/interfaces/ICache.html). Useful for mobile apps (e.g. React
    Native).

  Default: `memory`

- `auth0LogInMethod: Auth0LogInMethod`: Possible values are:

  - `popup`: Open Auth0's authentication page on a popup window while the original page just waits for authentication
    to take place or to timeout. This option is faster and less intrusive.

  - `redirect`: Navigate to Auth0's authentication page, which will redirect users back to your site or
    `auth0RedirectURI` upon authentication. Once they are redirected back, the URL will show a `code` and `state`
    query parameters for a second or two, until the authentication flow is completed.

  See: https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#loginWithRedirect,
  https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#handleRedirectCallback,
  https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#loginWithPopup

  Default: `popup`

- `auth0RedirectURI: Auth0RedirectUri | null`: Auth0's callback URL (`redirect_uri`) used during the authentication
  flow.

  See https://auth0.com/docs/authenticate/login/redirect-users-after-login

  Default: `location.origin` (when available in the platform)

- `auth0ReturnToURI: Auth0RedirectUri | null` Auth0's logout URL (`returnTo`) used during the logout flow.

  See https://auth0.com/docs/authenticate/login/logout/redirect-users-after-logout

  Default: `location.origin` (when available in the platform)

- `auth0RefreshTokenExpirationMs: number`: Refresh token expiration in milliseconds. This should/must match the value
  set in Auth0. On the client, this value is only used to set a timer to automatically log out users when their refresh
  token expires. Incorrectly setting this value will make users think they are still logged in, even after their refresh
  token expires (until they try to perform any kind of action through Othent and get an error).
   
  Default: `1296000000` (2 weeks)

- `autoConnect: AutoConnect`: Possible values are:

  - `eager`: Try to log in as soon as the page loads. This won't work when using `auth0Strategy = "refresh-memory"`.

  - `lazy` Try to log in as soon as there's an attempt to perform any action through Othent. This will only work with
    `auth0Strategy = "refresh-memory"` if the first action is preceded by a user action (e.g. click on a button).

  - `off`: Do not log in automatically. Trying to perform any action through Othent before calling `connect()` or
    `requireAuth()` will result in an error.

  Default: `lazy`

- `throwErrors: boolean`: All `Othent` methods could throw an error, so you should wrap them in `try-catch` blocks.
  Alternatively, you can set this option to `false` and the library will do this automatically, so no method will ever
  throw an error. In this case, however, you must add at least one error event listener with
  `othent.addEventListener("error", () => { ... })`.

  Default: `true`

- `tags: TagData[]`: Additional tags to include in transactions signed or sent using `Othent.sign`, `Othent.dispatch` or
  `Othent.signDataItem`.
  
  Default: `[]`

## Error Handling

All public `Othent` methods, except for the getters and properties, can throw an error when called under various
circumstances, so you should wrap them in `try-catch` blocks and handle errors appropriately.

Alternatively, you can set `throwErrors = false` to let `Othent` wrap all functions in `try-catch` blocks automatically.
In this case, you must subscribe to `error` events using the `addEventListener()` function:

```ts
const othent = new Othent({ throwErrors: false });

othent.addEventListener("error", (err) => {
  // TODO: Handle error...
});

// This will throw an error:
othent.sign({ foo: "bar" } as unknown as Transaction);
```

> TODO: Document custom error class and error types.

## Events

You can subscribe and unsubscribe to two different types of events from Othent (`auth` and `error`), using the
`addEventListener()` and `removeEventListener()` functions, respectively.

Additionally, `addEventListener()` returns a cleanup function that, when called, removes the event listener it created.

### Auth Event:

```ts
const othent = new Othent({ throwErrors: false });

othent.addEventListener("auth", (userDetails: UserDetails | null, isAuthenticated: boolean) => {
  // If `userDetails != null` and `isAuthenticated = false`, this value comes from the cache.
});

othent.connect();
```

### Error Event:

```ts
const othent = new Othent({ throwErrors: false });

othent.addEventListener("error", (err) => {
  // TODO: Handle error...
});

// This will throw an error:
othent.sign({ foo: "bar" } as unknown as Transaction);
```
Note that `error` type events are only fired when you set `throwErrors = false`.

See [Error Handling](#error-handling) above.

## TypeScript Support

TypeScript types are included in the `@othent/kms` package. On top of the `Othent` `class`, these are all the types
exported from `@othent/kms`:

> TODO: List exported types...
