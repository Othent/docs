---
description: https://github.com/Othent/package
---

# 🥪 SDK

The Othent Library is a collection of functions that enable interaction with the Othent walletless protocol. These functions are designed to make it seamless for developers to integrate Othent into their applications.

### Installation

To use the library in your project, you can install it using npm:

```javascript
npm i othent
```

### Usage

To use the library, you can import it into your project:

```javascript
import { Othent } from 'othent';
```

### Initialise Othent

You can generate your API key and API ID from [Othent.io](https://othent.io)

```javascript

// Initialise Othent

const othent = await Othent({ API_KEY, API_ID })

```

### Functions

**The following functions are available in the Othent Library:**

_**ping()**: Ping the Othent server._

```javascript

// Ping Othent

const response = await othent.ping();

console.log(response);

```

_**logIn()**: Log in a user and return their details._

```javascript

// Log in / create account

const userDetails = await othent.logIn();

console.log(userDetails);

```

_**logOut()**: Log out the current user._

```javascript

// Log out

const response = await othent.logOut();

console.log(response);

```

_**userDetails()**: Retrieve the details of the current user._

```javascript

// User details

const userDetails = await othent.userDetails();

console.log(userDetails);

```

_**readContract()**: Read data from the current user's contract._

```javascript

// Read contract

const contract = await othent.readContract();

console.log(contract);

```

_**readCustomContract({contract\_id})**: Read a custom contract._

```javascript

// Read custom contract

const contract_id = '2W9NoIJM1SuaFUaSOJsui_5lD_NvCHTjez5HKe2SjYU'

const contract = await othent.readCustomContract({contract_id});

console.log(contract);

```

_**signTransactionArweave({ othentFunction, data, tags })**: Sign a Arweave transaction._

```javascript

// Sign transaction Arweave

const signedArweaveTransaction = await othent.signTransactionArweave({
    othentFunction: 'uploadData', 
    data: file,
    tags: [ {name: 'Test', value: 'Tag'} ]
});

console.log(signedArweaveTransaction);

```

_**sendTransactionArweave(signedArweaveTransaction)**: Send a Arweave transaction._

<pre class="language-javascript"><code class="lang-javascript">
// Send transaction Arweave

const transaction = await othent.sendTransactionArweave(signedArweaveTransaction);

console.log<a data-footnote-ref href="#user-content-fn-1">(</a>transaction)

</code></pre>

_**signTransactionBundlr({ othentFunction, data, tags })**: Sign a Bundlr transaction._

```javascript

// Sign transaction Bundlr

const signedBundlrTransaction = await othent.signTransactionBundlr({
    othentFunction: 'uploadData', 
    data: file,
    tags: [ {name: 'Test', value: 'Tag'} ]
});

console.log(signedBundlrTransaction);

```

_**sendTransactionBundlr(signedBundlrTransaction)**: Send a Bundlr transaction._

<pre class="language-javascript"><code class="lang-javascript">
// Send transaction Bundlr

const transaction = await othent.sendTransactionBundlr(signedBundlrTransaction);

console.log<a data-footnote-ref href="#user-content-fn-2">(</a>transaction)

</code></pre>

_**signTransactionWarp({ othentFunction, data: {toContractId, toContractFunction, txnData}, tags })**: Sign a Warp transaction._

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

_**sendTransactionWarp(signedWarpTransaction)**: Send a Warp transaction._

```javascript

// Send transaction Warp

const transaction = await othent.sendTransactionWarp(signedWarpTransaction);

console.log(transaction)

```

_**initializeJWK({JWK\_public\_key})**: backup a Othent account with a JWK public key._

```javascript

// Initalize JWK to user

const transaction = await othent.initializeJWK({JWK_public_key});

console.log(transaction);

```

_**JWKBackupTxn({JWK\_signed\_JWT})**: Send a transaction with the specified JWK._

```javascript

// JWK backup transaction

const transaction = await othent.JWKBackupTxn({JWK_signed_JWT});

console.log(transaction);
  
```

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

### Contact

If you have any questions or issues with the SDK, please contact us at [hello@othent.io](mailto:hello@othent.io) or open an issue in the GitHub repository at [https://github.com/Othent](https://github.com/Othent/package).

### License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.

[^1]: 

[^2]: 
