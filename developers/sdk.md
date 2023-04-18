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
import othent from 'othent';
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

<pre class="language-javascript"><code class="lang-javascript">// Send transaction Arweave

const transaction = await othent.sendTransactionArweave(signedArweaveTransaction);
console.log<a data-footnote-ref href="#user-content-fn-1">(</a>transaction)

</code></pre>

_**signTransactionWarp({ othentFunction, data: {toContractId, toContractFunction, txnData}, tags })**: Sign a Warp transaction._

```javascript
// Sign transaction Warp

const signedWarpTransaction = await othent.signTransactionWarp({
  othentFunction: 'sendTransaction', 
  data: {
    toContractId: 'XL_AtkccUxD45_Be76Qe_lSt8q9amgEO9OQnhIo-2xI', 
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

### Contact

If you have any questions or issues with the SDK, please contact us at [hello@othent.io](mailto:hello@othent.io) or open an issue in the GitHub repository at [https://github.com/Othent](https://github.com/Othent/package).

### License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.

[^1]: 
