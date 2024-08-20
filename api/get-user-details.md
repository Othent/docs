---
description: Othent JS SDK getUserDetails() function
---

# Get User Details

Returns an object with all the user details (`UserDetails`) of the active (authenticated) user account:

- `authSystem`: The authentication protocol used (this will always be `"KMS"`).
- `email`: The connected user’s email address.
- `email_verified`: This field is set to `true` when the user successfully verifies their email address by clicking a verification link sent to their email.
- `family_name`: The last name or surname associated with the connected user.
- `given_name`: The first name associated with the connected user.
- `locale`: The connected user’s language preferences.
- `name`: The full name of the connected user created by the concatenation of the `given_name` and `family_name`.
- `nickname`: A less formal or preferred name for the connected user.
- `owner`: Every user account has an associated Arweave wallet. This is the public key of the associated Arweave wallet.
- `picture`: The image URL of the profile picture of the connected user account.
- `sub`: Every user account has an associated oauth account that facilitates the connection. This is the `id` of that oauth account.
- `walletAddress`: Every user account has an associated Arweave wallet. This is the wallet address of the associated Arweave wallet.

## API

```ts
getUserDetails(): Promise<UserDetails | null>;
```

### `return Promise<UserDetails | null>`

A `Promise` containing all the user details of the active user, or `null` if the user is not authenticated.

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

// Make sure the user is authenticated, or prompt them to authenticate:
await othent.requireAuth();

// Obtain the user's details:
const userDetails = await othent.getUserDetails();

console.log(`This is all the information a dApp can get from you ${ JSON.stringify(userDetails, null, '  ') }.`);
```
