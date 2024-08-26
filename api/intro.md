---
description: Using @othent/kms
---

# 🥪 Othent JS SDK

The Othent JS SDK exports a TypeScript `class` `Othent` that exposes a collection of functions that enable interaction
with wallet under Othent's custody. These functions are designed to make it seamless for developers to integrate Othent
into their applications, and closely follow [_ArConnect_'s API](https://docs.arconnect.io/) to provide a familiar
interface.

## Installation & Setup

To use the library in your project, you first need to install it using `npm` / `pnpm` / `yarn`:

```bash
npm i @othent/kms
pnpm i @othent/kms
yarn add @othent/kms
```

{% hint style="warning" %}
Make sure peer dependencies (`arweave`, `axios` and `warp-arbundles`) are also installed.
{% endhint %}

{% hint style="info" %}
TypeScript types are included in the `@othent/kms` package. You can find an exhaustive list in
[TypeScript Types](./typescript-types.md).
{% endhint %}

Next, simply instantiate `Othent` with [any options you need](./constructor.md):

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, ... });
```

Additionally, if you set the [`persistLocalStorage`](./constructor.md#persistlocalstorage-boolean--othentstoragekey)
option to persist and/or sync user details across tabs, you need to call [`startTabSynching`](./start-tab-synching.md)
and make sure the cleanup function it returns is called once you no longer need the `Othent` instance you've created.

Here's an example inside a React component:

```ts
import { Othent } from "@othent/kms";

const MyComponent = () => {
  const othent = useMemo(() => {
    return new Othent(options);
  }, [options]);

  useEffect(() => {
      const cleanupFn = othent.startTabSynching();

      return () => {
        cleanupFn();
      };
  }, [othent])
}
```

{% hint style="warning" %}
To use Othent in production, you'll have to reach out to the [Othent team on Discord](https://discord.gg/gWDmJep5)
to get your domain whitelisted.
{% endhint %}

### React

If you are using Othent with React, you might want to consider using
[React's Context](https://react.dev/learn/passing-data-deeply-with-context) to use a single `Othent` instance for your
whole app, or decoupling it even more by using a state management library like [MobX](https://mobx.js.org/README.html),
[TanStack Query](https://tanstack.com/query/latest) or [Redux](https://redux.js.org/). 

Alternatively, you might prefer to use [ArweaveKit](https://docs.arweavekit.com/wallets/wallet-kit). See
[Indirect Usage (through ArweaveKit)](#indirect-usage-through-arweavekit) below.

### React Native

Othent directly uses the [Web/Node.js Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Crypto) to create
hashes, verify signatures and, indirectly, through [`arweave-js`](https://github.com/ArweaveTeam/arweave-js). If your
environment doesn't has this API natively, you'll have to polyfill it.

Next, update your platform-specific configuration files to work with Auth0:

- See ["Integrate Auth0 in Your Application"](https://auth0.com/docs/quickstart/native/react-native/00-login#integrate-auth0-in-your-application)
  to update your `build.gradle` and `AppDelegate.mm` files. Othent's Auth0 domain is `auth.othent.io`.

- See ["Configure Callback and Logout URLs"](https://auth0.com/docs/quickstart/native/react-native/00-login#configure-callback-and-logout-urls)
  to define your callback and logout URLs. They should look something like this, for Android and iOS, respectively:

      {PACKAGE_NAME}.auth0://{YOUR_DOMAIN}/android/{PACKAGE_NAME}/callback
      {BUNDLE_IDENTIFIER}.auth0://{YOUR_DOMAIN}/ios/{BUNDLE_IDENTIFIER}/callback
  
Then, you need to set (at least) the following options when instantiating `Othent`:

- `auth0LogInMethod = "redirect"`
- `auth0RedirectURI` (callback URL): Based on the values defined above.
- `auth0ReturnToURI` (log out URL): Based on the values defined above.
- `auth0Cache`: You have to pass a custom [`ICache`](https://auth0.github.io/auth0-spa-js/interfaces/ICache.html)
  implementation. This object will be responsible of persisting the refresh tokens, so, on iOS, we recommend
  implementing it using [Keychain Services](https://developer.apple.com/documentation/security/keychain_services/).

Lastly, make sure when Auth0 redirects the user back to your app (`auth0RedirectURI`), you call
[`completeConnectionAfterRedirect`](./complete-connection-after-redirect.md), passing the URI with the `code` and
`state` params provided by Auth0, which handles the redirect callback.

See [Auth0's `handleRedirectCallback`](https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#handleRedirectCallback).

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

new Othent({ appInfo, inject: true, ... });

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

[Arweave Wallet Kit](https://docs.arweavekit.com/wallets/wallet-kit) provides a set of React Hooks and Components for
better interaction with Arweave wallets.

Note, however, that there might be some limitations, like some methods like `signDataItem`, `signMessage` or
`verifyMessage` not being (currently) available.

{% hint style="warning" %}
TODO: We are still working on this. We'll update the documentation soon.
{% endhint %}

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
import { Othent, AppInfo } from "@othent/kms";

const appInfo: AppInfo = {
  name: "My Awesome App",
  version: "1.0.0",
  env: "production",
};

const othent = new Othent({ appInfo, throwErrors: false, ... });

othent.addEventLister("error", (err) => {
  console.error(err);
});

await othent.connect();

const mySecret = await othent.encrypt("My secret");

const transaction = await arweave.createTransaction({
  data: mySecret,
});

const result = await othent.dispatch(transaction);
const transactionURL = `https://viewblock.io/arweave/tx/${result.id}`;

console.log(transactionURL);
```