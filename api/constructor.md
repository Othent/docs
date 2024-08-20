---
description: Othent JS SDK constructor() function
---

# Constructor

Instantiate `Othent`.

## API

```ts
constructor(
  options: OthentOptions,
): Othent;
```

### `options: OthentOptions`

Options to customize `Othent`'s behavior when instantiating it.

{% hint style="info" %}
Take a look at the [TypeScript `OthentOptions` and `OthentConfig` interfaces on GitHub](https://github.com/Othent/KeyManagementService/blob/main/src/lib/config/config.types.ts)
for additional details.
{% endhint %}

The following options are available:

- #### `appName: string`

  Name of your app. This will add a tag `App-Name: <appName>` to any transaction signed or sent using `Othent.sign`,
  `Othent.dispatch` or `Othent.signDataItem`.

- #### `appVersion: string`

  Version of your app. This will add a tag `App-Version: <appVersion>` to any transaction signed or sent using
  `Othent.sign`, `Othent.dispatch` or `Othent.signDataItem`.

- #### `persistCookie: boolean | OthentStorageKey`
  
  _Default_: `false`

  Set this to `true` or the name of the cookie where you'd like the user details JSON to be stored.
  
  Note setting this option to `true` will set the cookie on the client / frontend, but it won't recover it on the server /
  backend. If you are using SSR, you need to use `cookie = true` in conjunction with `initialUserDetails`.

- #### `persistLocalStorage: boolean | OthentStorageKey`

  _Default_: `false`

  Set this to `true` or the name of the `localStorage` item where you'd like the user details JSON to be stored.
  
  Note the stored values will be removed / discarded if more than `refreshTokenExpirationMs` have passed, but will remain
  in `localStorage` until then or until the user logs out.

- #### `gatewayConfig?: GatewayConfig`

  Gateway config to connect to Arweave.

- #### `initialUserDetails?: UserDetails | null`

  Initial user details. Useful for server-side rendered sites or native apps that might store the most recent user details
  externally (e.g. cookie or `SharedPreferences`).

- #### `debug: boolean`

  _Default_: `false`

  Enable additional logs.

- #### `inject: boolean`

  _Default_: `false`

  Inject Othent's instance as `window.arweaveWallet` so that `arweave-js` can use it on the background.

- #### `serverBaseURL: string`

  API base URL. Needed if you are using a private/self-hosted API and Auth0 tenant.

- #### `auth0Domain: string`

  Auth0 domain. Needed if you are using a private/self-hosted API and Auth0 tenant.

- #### `auth0ClientId: string`

  Auth0 client ID. Needed if you are using a private/self-hosted API and Auth0 tenant, or if you have a dedicated App
inside Othent's Auth0 tenant to personalize the logic experience (premium subscription).

- #### `auth0Strategy: Auth0Strategy`

  _Default_: `memory`

  Possible values are:
    
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

- #### `auth0LogInMethod: Auth0LogInMethod`

  _Default_: `popup`

  Possible values are:

  - `popup`: Open Auth0's authentication page on a popup window while the original page just waits for authentication
    to take place or to timeout. This option is faster and less intrusive.

  - `redirect`: Navigate to Auth0's authentication page, which will redirect users back to your site or
    `auth0RedirectURI` upon authentication. Once they are redirected back, the URL will show a `code` and `state`
    query parameters for a second or two, until the authentication flow is completed.

    See: [`loginWithRedirect`](https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#loginWithRedirect),
[`handleRedirectCallback`](https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#handleRedirectCallback),
[`loginWithPopup`](https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#loginWithPopup).

- #### `auth0RedirectURI: Auth0RedirectUri | null`

  _Default_: `location.origin`** (when available in the platfor

  Auth0's callback URL (`redirect_uri`) used during the authentication flow.

  See https://auth0.com/docs/authenticate/login/redirect-users-after-login

- #### `auth0ReturnToURI: Auth0RedirectUri | null`

  _Default_: `location.origin`** (when available in the platfor

  Auth0's logout URL (`returnTo`) used during the logout flow.

  See https://auth0.com/docs/authenticate/login/logout/redirect-users-after-logout

- #### `auth0RefreshTokenExpirationMs: number`:
   
  _Default_: `1296000000` (2 weeks)

  Refresh token expiration in milliseconds. This should/must match the value set in Auth0. On the client, this value is
  only used to set a timer to automatically log out users when their refresh token expires. Incorrectly setting this value
  will make users think they are still logged in, even after their refresh token expires (until they try to perform any
  kind of action through Othent and get an error).

- #### `autoConnect: AutoConnect`

  _Default_: `lazy`

  Possible values are:

  - `eager`: Try to log in as soon as the page loads. This won't work when using `auth0Strategy = "refresh-memory"`.

  - `lazy` Try to log in as soon as there's an attempt to perform any action through Othent. This will only work with
    `auth0Strategy = "refresh-memory"` if the first action is preceded by a user action (e.g. click on a button).

  - `off`: Do not log in automatically. Trying to perform any action through Othent before calling `connect()` or
    `requireAuth()` will result in an error.

- #### `throwErrors: boolean`

  _Default_: `true`
 
  All `Othent` methods could throw an error, so you should wrap them in `try-catch` blocks. Alternatively, you can set
  this option to `false` and the library will do this automatically, so no method will ever throw an error. In this case,
  however, you must add at least one error event listener with `othent.addEventListener("error", () => { ... })`.

- #### `tags: TagData[]`
  
  _Default_: `[]`

  Additional tags to include in transactions signed or sent using `Othent.sign`, `Othent.dispatch` or `Othent.signDataItem`.