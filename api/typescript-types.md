---
description: Othent exported TypeScript types.
---

## TypeScript Types

### [`othent.types.ts`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/othent/othent.types.ts)

#### Events

See [Events](./events.md).

```ts
type OthentEventType = "auth" | "error"
```

```ts
type AuthListener = (
    userDetails: UserDetails | null,
    isAuthenticated: boolean,
) => void;
```

```ts
type ErrorListener = (err: Error | OthentError) => void;
```

#### Dispatch

See [`dispatch()`](./dispatch.md);

```ts
interface DispatchOptions {
  arweave?: Arweave;
  node?: UrlString;
}
```

```ts
interface ArDriveBundledTransactionResponseData {
  id: string;
  timestamp: number;
  winc: string;
  version: string;
  deadlineHeight: number;
  dataCaches: string[];
  fastFinalityIndexes: string[];
  public: string;
  signature: string;
  owner: string;
}
```

```ts
interface ArDriveBundledTransactionData
  extends ArDriveBundledTransactionResponseData {
  type: "BUNDLED";
}
```

```ts
interface UploadedTransactionData {
  type: "BASE";
  id: string;
  signature: string;
  owner: string;
}
```

#### `DataItem`

See [`signDataItem()`](./sign-data-item.md);

```ts
type OthentEventType = "auth" | "error";
```

```ts
interface TagData {
  name: string;
  value: string;
}
```

```ts
interface DataItem {
  data: string | Uint8Array;
  target?: string;
  anchor?: string;
  tags?: TagData[];
}
```

### [`config.types`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/config/config.types.ts)

See [`constructor()`](./constructor.md#appinfo-appinfo) and [`config`](./config.md).

```ts
type OthentStorageKey = `othent${string}`;
```

```ts
type Auth0Strategy = "cross-site-cookies" | "refresh-tokens";
```

```ts
type Auth0Cache = "memory" | "localstorage" | ICache;
```

```ts
type Auth0CacheType = "memory" | "localstorage" | "custom";
```

```ts
type Auth0RedirectUri =
  | UrlString
  | `${string}.auth0://${string}/ios/${string}/callback`
  | `${string}.auth0://${string}/android/${string}/callback`;
```

```ts
type Auth0RedirectUriWithParams = `${Auth0RedirectUri}?${string}`;
```

```ts
type Auth0LogInMethod = "popup" | "redirect";
```

```ts
type AutoConnect = "eager" | "lazy" | "off";
```

```ts
interface AppInfo {
  name: string;
  version: string;
  env: string;
  logo?: UrlString;
}
```

```ts
interface OthentConfig { ... } // Listed in constructor()'s docs page.
```

```ts
interface OthentOptions { ... } // Listed in constructor()'s docs page.
```

### [`auth0.types.ts`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/auth0/auth0.types.ts)

See [`getUserDetails()`](./get-user-details.md#return-promiseuserdetails--null).

```ts
type Auth0Provider =
  | `apple`
  | `auth0`
  | `google-oauth2`
  | `<LinkedIn>`
  | `<X>`
  | `<Meta>`
  | `<Twitch>`
  | `github`;
```

```ts
type Auth0Sub = `${Auth0Provider}|(${string})`;
```

```ts
type Auth0ProviderLabel =
  | `Apple`
  | `E-Mail`
  | `Google`
  | `LinkedIn`
  | `X`
  | `Meta`
  | `Twitch`
  | `GitHub`
  | `Unknown Provider`;
```

```ts
type Auth0WalletAddressLabel = `${Auth0ProviderLabel} (${string})`;
```

```ts
type ANSDomain = `${string}.ar`;
```

```ts
type OthentWalletAddressLabel = Auth0WalletAddressLabel | ANSDomain;
```

```ts
export interface UserDetails {
  // Default from Auth0's User:
  sub: Auth0Sub;
  name: string;
  givenName: string;
  middleName: string;
  familyName: string;
  nickname: string;
  preferredUsername: string;
  profile: string;
  picture: string;
  website: string;
  locale: string;
  updatedAt: string;
  email: string;
  emailVerified: boolean;

  // Custom from Auth0's Add User Metadata action:
  owner: B64UrlString;
  walletAddress: B64UrlString;
  walletAddressLabel: OthentWalletAddressLabel;
  authSystem: "KMS";
  authProvider: Auth0Provider;
}
```

### [`common.types.ts`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/othent-kms-client/operations/common.types.ts)

These types are only exported for backwards compatibility with `@othent/kms` version `1.X.X` and to facilitate the
migration to version 2 for those that might have stored this `BufferObject` entity.

```ts
interface BufferObject {
  type: "Buffer";
  data: number[];
}
```

```ts
function isBufferObject(obj: any): obj is BufferObject {
  return (
    obj.type === "Buffer" &&
    Array.isArray(obj.data) &&
    typeof obj[0] === "number"
  );
}
```

### [`arconnect.types.ts`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/utils/arconnect/arconnect.types.ts)

Note that the `DispatchResult`, `AppInfo` and `DateItem` types defined in
[`arconnect` / `arconnectio/types`](https://github.com/arconnectio/types) are not exported as Othent overrides and
extends them.

```ts
type PermissionType =
  | "ACCESS_ADDRESS"
  | "ACCESS_PUBLIC_KEY"
  | "ACCESS_ALL_ADDRESSES"
  | "SIGN_TRANSACTION"
  | "ENCRYPT"
  | "DECRYPT"
  | "SIGNATURE"
  | "ACCESS_ARWEAVE_CONFIG"
  | "DISPATCH";
```

```ts
interface GatewayConfig {
  host: string;
  port: number;
  protocol: "http" | "https";
}
```

```ts
interface SignMessageOptions {
  hashAlgorithm?: "SHA-256" | "SHA-384" | "SHA-512";
}
```

### [`error.ts`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/utils/errors/error.ts)

An `enum OthentErrorID` and `class OthentError` (`extends Error`) are exported from `error.ts`.

See [Error Handling](./error-handling.md).

### [`url.types`](https://github.com/Othent/KeyManagementService/blob/main/src/lib/utils/typescript/url.types.ts)

```ts
type UrlString = `http://${string}` | `https://${string}`;
```