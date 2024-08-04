---
description: Othent JS SDK connect() function
---

# Connect

Prompts the user to sign in/up (connects the user's wallet) using
[_Auth0_'s popup](https://auth0.com/docs/libraries/lock/lock-authentication-modes#popup-mode).

Note that while `connect()`'s function signature is identical to that of
[_ArConnect_'s `connect()`](https://docs.arconnect.io/api/connect), you don't need to request permissions from the user to
interact with their wallets, as it's already implicit that users are giving _Othent_ full control of their wallet.

This function will throw an error in the following cases:

- When passing `permissions` different to `undefined` and the default value  (all permissions). While that parameter has
  been added for signature compatibility with _ArConnect_ and other wallets, _Othent_ implicitly requires all
  permissions. Passing anything else will throw an error.

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

| Argument      | Type                                                       | Description                                                                       |
| ------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `permissions` | [`Array<PermissionType>`](connect.md#permissions)          | An array of permission to request from the user (at least one has to be included) |
| `appInfo?`    | [`AppInfo`](connect.md#additional-application-information) | Additional information about the app                                              |
| `gateway?`    | [`Gateway`](connect.md#custom-gateway-config)              | Custom gateway config                                                             |

**Returns:** A Promise with the `UserDetails` or `null` if the log in modal was closed, could not even be opened or authentication failed.

{% hint style="info" %}
The `appInfo` argument is optional. If it is not provided, the SDK will use the `appInfo` provided when you instantiated it.
{% endhint %}

{% hint style="info" %}
The `gateway` argument is optional. If it is not provided, the SDK will use the default `arweave.net` gateway.
{% endhint %}

## Permissions

These are all the permissions Othent implicitly requires from the user for each interaction that involves the usage of
their wallet:

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

## Additional application information

You can provide your application's name and version to the SDK. These two values are required when instantiating the SDK
and will be added as tags (`App-Version: <appVersion>` and `App-Version: <appVersion>`, respectively) to any transaction
signed or sent using `Othent.sign`, `Othent.dispatch` or `Othent.signDataItem`.


```ts
interface AppInfo {
  name?: string;     // optional application name
  version?: string;  // optional application version
}
```

## Custom gateway config

If your application requires the usage of a special gateway or you want to test with an
[ArLocal](https://github.com/textury/arlocal) testnet gateway, you'll have to provide some information about it when
connecting to Othent's SDK.

```ts
interface Gateway {
  host: string;
  port: number;
  protocol: "http" | "https";
}
```

## Example usage

```ts
// connect to the extension
await othent.connect(
  // all permissions are implicit regardless
  undefined
  // provide some extra info for our app
  {
    name: "Super Cool App",
    version: "1.0.12"
  },
  // custom gateway
  {
    host: "g8way.io",
    port: 443,
    protocol: "https"
  }
);
```
