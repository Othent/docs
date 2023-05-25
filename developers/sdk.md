---
description: https://github.com/Othent/package
---

# 🥪 SDK

The Othent Library is a collection of functions that enable interaction with the Othent walletless protocol. These functions are designed to make it seamless for developers to integrate Othent into their applications.

## Installation

To use the library in your project, you can install it using npm:

```javascript
npm i othent
```

## Usage

To use the library, you can import it into your project:

```javascript
import { Othent } from 'othent';
```

## Initialise Othent

You can generate your API ID from [Othent.io](https://othent.io)

```javascript

// Initialise Othent

const othent = await Othent({ API_ID })

```

## Functions

**The following functions are available in the Othent Library:**

### Connect

#### ping

_Ping the Othent server._

```javascript

// Ping Othent

const response = await othent.ping();

console.log(response);

```

#### logIn

_Log in a user and return their details._

```javascript

// Log in / create account

const userDetails = await othent.logIn();

console.log(userDetails);

```

#### logOut

_Log out the current user._

```javascript

// Log out

const response = await othent.logOut();

console.log(response);

```

#### userDetails

_Retrieve the details of the current user._

```javascript

// User details

const userDetails = await othent.userDetails();

console.log(userDetails);

```

### Contracts

#### readContract

_Read data from the current user's contract._

```javascript

// Read contract

const contract = await othent.readContract();

console.log(contract);

```

#### readCustomContract

_Read a custom contract by its `contract_id`. Receives an object with only one member of type `string` called `contract_id`_

```javascript

// Read custom contract

const contract_id = '2W9NoIJM1SuaFUaSOJsui_5lD_NvCHTjez5HKe2SjYU'

const contract = await othent.readCustomContract({contract_id});

console.log(contract);

```

### Arweave Transactions

#### signTransactionArweave

_Sign an Arweave transaction. It receives an object with 3 members:_

* `othentFunction`: action to be performed. Type `string`.
* `data`: Data to be attached to the function.
* `tags`: Array of objects with a `{ name: string, value: string}` structure.

```javascript

// Sign transaction Arweave

const signedArweaveTransaction = await othent.signTransactionArweave({
  othentFunction: 'uploadData', 
    data: file,
    tags: [ {name: 'Test', value: 'Tag'} ]
});

console.log(signedArweaveTransaction);

```

#### sendTransactionArweave

_Send an Arweave transaction. Receives a signed Arweave transaction object like the one returned from the `signTransactionArweave` function above._

```javascript

// Send transaction Arweave

const transaction = await othent.sendTransactionArweave(signedArweaveTransaction);

console.log(transaction)

```

### Bundlr Transactions

#### signTransactionBundlr

_Sign a Bundlr transaction. It receives an object with 3 members:_

* `othentFunction`: action to be performed. Type `string`.
* `data`: Data to be attached to the function.
* `tags`: Array of objects with a `{ name: string, value: string}` structure.

```javascript

// Sign transaction Bundlr

const signedBundlrTransaction = await othent.signTransactionBundlr({
    othentFunction: 'uploadData', 
    data: file,
    tags: [ {name: 'Test', value: 'Tag'} ]
});

console.log(signedBundlrTransaction);

```

#### sendTransactionBundlr

_Send a Bundlr transaction. Receives a signed Bundlr transaction object like the one returned from the `signTransactionBundlr` function above._

```javascript

// Send transaction Bundlr

const transaction = await othent.sendTransactionBundlr(signedBundlrTransaction);

console.log(transaction)

```

### Warp Transactions

#### signTransactionWarp

_Sign a Bundlr transaction. It receives an object with 3 members:_

* `othentFunction`: action to be performed. Type `string`.
* `data`: An object containing 3 members:
  * `toContractid`: A `string` with the Warp contract Id.
  * `toContractFunction`: A `string` with the function name from the Warp contract to call.
  * `txnData`: The data object that the mentioned function receives.
* `tags`: Array of objects with a `{ name: string, value: string}` structure.

```javascript

// Sign transaction Warp

const signedWarpTransaction = await othent.signTransactionWarp({
  othentFunction: 'sendTransaction', 
  data: {
    toContractId: '2W9NoIJM1SuaFUaSOJsui_5lD_NvCHTjez5HKe2SjYU', 
    toContractFunction: 'createPost', 
    txnData: { blog_entry: 'Hello World!'} 
  }, 
  tags: [ {name: 'Test', value: 'Tag'} ]
});

console.log(signedWarpTransaction);

```

#### sendTransactionWarp

_Send a Warp transaction. Receives a signed Warp transaction object like the one returned from the `signTransactionWarp` function above._

```javascript

// Send transaction Warp

const transaction = await othent.sendTransactionWarp(signedWarpTransaction);

console.log(transaction)

```

### Utilities

#### initializeJWK

_Backup an Othent account with a JWK public key through the ArConnect pop up._

```javascript

// Initalize JWK to user

const transaction = await othent.initializeJWK();

console.log(transaction);

```

#### JWKBackupTxn

_Send a transaction with the specified JWK. It receives a `{ JWK_signed_JWT }` object._

```javascript

// JWK backup transaction

const transaction = await othent.JWKBackupTxn({JWK_signed_JWT});

console.log(transaction);
  
```

## Examples

_**How to generate a JWT signed by a JWK**_

```javascript

// JWT signed by your own JWK

const jwt = require('jsonwebtoken');
const jwkToPem = require('jwk-to-pem')

const private_pem = jwkToPem(jwk, {private: true});
const public_pem = jwkToPem(jwk);

const payload = {
  sub: 'google-oauth2|113378216876216346016',
  contract_id: 'Tb33ItPlttNYtABjMo03gK425vCcYYMX4c7i8W_I2X0',
  tags: [ {name: 'Test', value: 'Tag'} ],
  
  contract_input: {
    data: {
      toContractFunction: "createPost",
      toContractId: "2W9NoIJM1SuaFUaSOJsui_5lD_NvCHTjez5HKe2SjYU",
      txnData: { blog_post: "JWK TXN!" }
    },
    othentFunction: "JWKBackupTxn"
    },
  };
  
const options = {
    algorithm: 'RS256',
    expiresIn: '100000h',
    issuer: 'https://Othent.io'
  };
  
const JWT = jwt.sign(payload, private_pem, options);

console.log(JWT)

```

## Contact

If you have any questions or issues with the SDK, please contact us at [hello@othent.io](mailto:hello@othent.io) or open an issue in the GitHub repository at [https://github.com/Othent](https://github.com/Othent/package).

## License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.
