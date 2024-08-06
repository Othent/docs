---
description: https://github.com/Othent/package
---

# 🥪 Othent JS SDK

The Othent JS SDK is a `class` (`Othent`) that exposes a collection of functions that enable interaction with wallet
under Othent's custody. These functions are designed to make it seamless for developers to integrate Othent into their
applications, and closely follow [`ArConnect`'s API](https://docs.arconnect.io/) to provide a familiar interface.

## Installation

To use the library in your project, you can install it using `npm` / `pnpm` / `yarn`:

```bash
npm i othent
pnpm i othent
yarn i othent
```

### React Native

Othent directly uses the [Web/Node.js Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Crypto) to create hashes, verify signatures and, indirectly,
through [`arweave-js`](https://github.com/ArweaveTeam/arweave-js).

If you are in an environment where that API is not available, like React Native, you'll have to polyfill it.

TODO: Add step by step here.

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
import { Othent } from 'othent';

Othent({ inject: true, /* Additional Othent options */ });

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

- `crypto?: Crypto | null`: Crypto module needed for signing, if your environment doesn't provide one natively (e.g.
  React Native).

- `inject?: boolean`: Inject Othent's instance as `window.arweaveWallet` so that `arweave-js` can use it on the
  background.

- `serverBaseURL: string`: API base URL. Needed if you are using a private/self-hosted API and Auth0 tenant.

- `auth0Domain: string`: Auth0 domain. Needed if you are using a private/self-hosted API and Auth0 tenant.

- `auth0ClientId: string`: Auth0 client ID. Needed if you are using a private/self-hosted API and Auth0 tenant, or if
  you have a dedicated App inside Othent's Auth0 tenant to personalize the logic experience (premium subscription).

- `auth0Strategy: Auth0Strategy`: Possible values are:
    
  - `iframe-cookies`: Use cross-site cookies for authentication and store the cache in memory. Not recommended, as
    this won't work in browsers that block cross-site cookies, such as Brave.
    
  - `refresh-localstorage`: Use refresh tokens for authentication and store the cache in localStorage. This makes it
    possible for new tabs to automatically log in (with `autoConnect = "eager"`), even after up to 2 weeks of inactivity
    (i.e. "keep me logged in"), but offers a larger attack surface to attackers trying to get a hold of the refresh /
    access tokens.
    
  - `refresh-memory`: Use refresh tokens for authentication and store the cache in memory. This is the most secure and
    recommended option, but new tabs won't be able to automatically refresh the session without a previous user action
    (you cannot use `autoConnect = "eager"` with this option), as refresh tokens won't be persisted, so the only way to
    refresh the session is to open the authentication popup again once the user interacts with the page, which will
    immediately close if the user still has a valid session.
        
    However, by setting the `localStorage = true` option, the user details (but not the refresh / access tokens) will be
    persisted in `localStorage` until the last refresh token's expiration date, allowing you to read the user details
    (`.getUserDetails()` / `.getSyncUserDetails()`) and make it look in the UI as if the user were already logged in.
   
  Default: `refresh-memory`

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

TODO: error handling, error class

## Events

TODO: Mention special setup for events (event listeners, etc).

> ```ts
> addEventListener("arweaveWalletLoaded", () => {
>   console.log(`You are using the ${window.arweaveWallet.walletName} wallet.`);
>   console.log(`Wallet version is ${window.arweaveWallet.walletVersion}`);
> });
> ```
> 
> {% hint style="danger" %}
> **Please remember:** to interact with the API, make sure that the `arweaveWalletLoaded` event has already been fired. Read more about that [here](events.md#arweavewalletloaded-event). `const cleanupFn = othent.init();`
> {% endhint %}

## TypeScript Support

TypeScript types are included in the `@othent/kms` package. On top of the `Othent` `class`, these are all the types
exported from `@othent/kms`:

TODO: List exported types...

> Additional Injected API fields
> 
> The ArConnect Injected API provides some additional information about the extension. You can retrive the wallet version (`window.arweaveWallet.walletVersion`) and you can even verify that the currently used wallet API indeed belongs to ArConnect using the wallet name (`window.arweaveWallet.walletName`).
