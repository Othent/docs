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

try {
  const response = await othent.ping();
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**logIn()**: Log in a user and return their details._

```javascript
// Log in

try {
  const response = await othent.logIn();
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**logOut()**: Log out the current user._

```javascript
// Log out

try {
  const response = await othent.logOut();
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**userDetails()**: Retrieve the details of the current user._

```javascript
// User details

try {
  const response = await othent.userDetails();
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**readContract()**: Read data from the current user's contract._

```javascript
// Read contract

try {
  const response = await othent.readContract();
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**signTransaction({ method, data, tags })**: Sign a transaction with the current user's account._

```javascript
// Sign transaction


// Arweave transaction
async function arweaveTransaction(file) {
  try {
    const signedTransaction = await othent.signTransaction({
      method: 'arweave', 
      data: { 
        othentFunction: 'uploadData', 
        file: file
      }, 
      tags: [ {name: 'Test': value: 'Tag'} ]
    });
    console.log(signedTransaction);
  } catch (error) {
    console.error(error);
  }
}


// Warp transaction
async function warpTransaction() {
  try {
    const signedTransaction = await othent.signTransaction({
      method: 'warp', 
      data: { 
        othentFunction: 'sendTransaction', 
        toContractId: 'XL_AtkccUxD45_Be76Qe_lSt8q9amgEO9OQnhIo-2xI', 
        toContractFunction: 'createPost', 
        txnData: { blog_entry_18: 'Hello World!'} 
      }, 
      tags: [ {name: 'Test': value: 'Tag'} ]
    });
    console.log(signedTransaction);
  } catch (error) {
    console.error(error);
  }
}

```

_**sendTransaction(JWT)**: Send a signed transaction to Othent._

```javascript
// Send transaction

try {
  const response = await othent.sendTransaction(signedTransaction);
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**initializeJWK(JWK\_public\_key\_PEM)**: backup a Othent account with a JWK public key._

```javascript
// Initalize JWK to user

try {
  const response = await othent.initializeJWK(JWK_public_key_PEM );
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**JWKBackupTxn(JWT)**: Send a transaction with the specified JWK._

```javascript
// JWK backup transaction

try {
  const response = await othent.JWKBackupTxn(signedJWTByJWK );
  console.log(response);
} catch (error) {
  console.error(error);
}
```

### Contact

If you have any questions or issues with the SDK, please contact us at [hello@othent.io](mailto:hello@othent.io) or open an issue in the GitHub repository at [https://github.com/Othent](https://github.com/Othent/package).

### License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.
