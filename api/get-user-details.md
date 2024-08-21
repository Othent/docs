---
description: Othent JS SDK getUserDetails() function
---

# Get User Details

Returns an object with all the user details (`UserDetails`) of the active (authenticated) user account.

## API

```ts
getUserDetails(): Promise<UserDetails | null>;
```

### `return Promise<UserDetails | null>`

A `Promise` containing all the user details of the active user, or `null` if the user is not authenticated.

```ts
interface UserDetails {
  // Default from Auth0's User:

  /**
   * ID of the user's Auth0 account.
   */
  sub: Auth0Sub;

  /**
   * The full name of the connected user created by the concatenation of the `givenName` and `familyName`.
   */
  name: string;

  /**
   * The first name associated with the connected user.
   */
  givenName: string;

  /**
   * The middle name or surname associated with the connected user.
   */
  middleName: string;

  /**
   * The last name or surname associated with the connected user.
   */
  familyName: string;

  /**
   * A less formal nickname for the connected user.
   */
  nickname: string;

  /**
   * The preferred username for the connected user.
   */
  preferredUsername: string;

  /**
   * The image URL of the profile picture of the connected user account.
   */
  picture: string;

  /**
   * Website associated to the connected user, if any.
   */
  website: string;

  /**
   * Locale of the connected user.
   */
  locale: string;

  /**
   * Date when the connected user was last updated.
   */
  updatedAt: string;

  /**
   * The connected user’s email address.
   */
  email: string;

  /**
   * This field is set to `true` when the user successfully verifies their email address by clicking a verification
   * link sent to their email.
   */
  emailVerified: boolean;

  // Custom from Auth0's Add User Metadata action:

  /**
   * Every user account has an associated Arweave wallet. This is the public key of the associated Arweave wallet,
   * derived from `sub`.
   */
  owner: B64UrlString;

  /**
   * Every user account has an associated Arweave wallet. This is the wallet address of the associated Arweave wallet,
   * derived from `owner`,
   */
  walletAddress: B64UrlString;

  /**
   * The wallet address label. This is either coming from ANS or `"{Auth0Provider} ({email})"`.
   */
  walletAddressLabel: OthentWalletAddressLabel;

  /**
   * The authentication protocol used (this will always be "KMS").
   */
  authSystem: "KMS";

  /**
   * The authentication provider (social network, platform...) that was used to sign in.
   */
  authProvider: Auth0Provider;
}
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ appInfo, throwErrors: false, ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's details:
const userDetails = await othent.getUserDetails();

console.log(`This is all the information a dApp can get from you ${ JSON.stringify(userDetails, null, '  ') }.`);
```
