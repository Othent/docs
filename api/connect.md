---
description: Othent JS SDK connect() function
---

# Connect

Prompts the user to sign in/up (connects the user's wallet) using
[_Auth0_'s popup](https://auth0.com/docs/libraries/lock/lock-authentication-modes#popup-mode).

Note that while `connect()`'s function signature is identical to that of
[_ArConnect_'s `connect()`](https://docs.arconnect.io/api/connect), you don't need to request permissions from the user
to interact with their wallets, as _Othent_ implicitly requires all permissions.

{% hint style="danger" %}
**Caution:** Users using _Othent_ are giving dApps that use _Othent_ full control of their wallet.
{% endhint %}

This function will throw an error in the following cases:

- When passing `permissions` different to `undefined` and the default value (all permissions). Passing anything else
  will throw an error.

- When this function is called before the user interacts with the page (e.g. by clicking on a button), as that will
  result in a `Unable to open a popup` error.

- When the user closes the _Auth0_ popup before authenticating, as that will result in a `Popup closed` error.

- When authentication fails.

## API

```ts
connect(
  permissions?: PermissionType[],
  appInfo?: AppInfo,
  gateway?: GatewayConfig,
): Promise<UserDetails | null>;
```

### `permissions?: PermissionType[]`

An array of permission to request from the user, but only `undefined` or an array with all permissions are valid.
Passing anything else will throw an error.

| Permission              | Description                                                             |
| ----------------------- | ----------------------------------------------------------------------- |
| `ACCESS_ADDRESS`        | Allow the app to get the active wallet's address                        |
| `ACCESS_PUBLIC_KEY`     | Enable the app to access the active wallet's public key                 |
| `ACCESS_ALL_ADDRESSES`  | Enable the app to access all wallet addresses added to ArConnect        |
| `SIGN_TRANSACTION`      | Allow the app to sign an Arweave transaction (Base layer)               |
| `ENCRYPT`               | Enable the app to encrypt data with the user's wallet through ArConnect |
| `DECRYPT`               | Allow the app to decrypt data encrypted with the user's wallet          |
| `SIGNATURE`             | Allow the app to sign messages with the user's wallet through ArConnect |
| `ACCESS_ARWEAVE_CONFIG` | Enable the app to access the current gateway config                     |
| `DISPATCH`              | Allow the app to dispatch a transaction (bundle or base layer)          |

{% hint style="danger" %}
**Caution:** Users using _Othent_ are giving dApps that use _Othent_ full control of their wallet.
{% endhint %}

### `appInfo?: AppInfo`

You must provide your application's name and version, and optionally logo, to the SDK when instantiating it. These
values can also be changed when calling `connect()`, to make _Othent_ compatible with projects using _ArConnect_.

```ts
interface AppInfo {
  /**
   * Name of your app. This will add a tag `App-Name: <appName>` to any transaction signed or sent using `Othent.sign`,
   * `Othent.dispatch` or `Othent.signDataItem`.
   */
  name: string;

  /**
   * Version of your app. This will add a tag `App-Version: <appVersion>` to any transaction signed or sent using
   * `Othent.sign`, `Othent.dispatch` or `Othent.signDataItem`.
   */
  version: string;

  /**
   * Environment your app is currently running on (e.g. "development", "staging", "production", ...). This will add a
   * tag `App-Env: <appEnv>` to any transaction signed or sent using `Othent.sign`, `Othent.dispatch` or
   * `Othent.signDataItem`.
   *
   * If no value (empty `string`) is provided, this will automatically be set to `"development"` if
   * `location.hostname = "localhost"` or `"production"` otherwise.
   */
  env: string;

  /**
   * Image with the logo of your app. Optional and not used for now.
   */
  logo?: UrlString;
}
```

### `gateway?: GatewayConfig`

If your application requires the usage of a special gateway or you want to test with an
[ArLocal](https://github.com/textury/arlocal) testnet gateway, you'll have to provide some information about it when
connecting to Othent's SDK.

You can set this value when instantiating `Othent` and also change it when calling `connect()`, to make _Othent_
compatible with projects using _ArConnect_.

```ts
interface GatewayConfig {
  host: string;
  port: number;
  protocol: "http" | "https";
}
```

### `return Promise<UserDetails | null>`

A `Promise` with the `UserDetails` or `null` if the log in modal was closed, could not even be opened or authentication failed.

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

await othent.connect(
  // All permissions are implicit regardless:
  undefined

  // Provide some extra info for our app, if not provided to the constructor:
  {
    name: "Super Cool App",
    version: "1.0.12",
    env: "production",
  },
  
  // Custom gateway, if not provided to the constructor:
  {
    host: "g8way.io",
    port: 443,
    protocol: "https"
  }
);
```
