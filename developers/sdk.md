---
description: See code at https://github.com/Othent/package or live demo at SDK.Othent.io
---

# ⚙ SDK

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

_**signTransaction(othentFunction, toContractId, toContractFunction, txnData)**: Sign a transaction with the current user's account._

```javascript
// Sign transaction

const othentFunction = 'example_function';
const toContractId = 'example_contract_id';
const toContractFunction = 'example_contract_function';
const txnData = 'example_transaction_data';

try {
  const response = await othent.signTransaction(othentFunction, toContractId, toContractFunction, txnData);
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**sendTransaction(JWT)**: Send a signed transaction to Othent._

```javascript
// Send transaction

const JWT = 'example_jwt';

try {
  const response = await othent.sendTransaction(JWT);
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**uploadData(file)**: Upload a file to Arweave and create a Othent users files hash._

```javascript
// Upload data

const file = '';

try {
  const response = await othent.uploadData(file);
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**initializeJWK(JWK\_public\_key\_PEM)**: backup a Othent account with a JWK public key._

```javascript
// Initalize JWK

const JWK_public_key_PEM = 'example_public_key_pem';

try {
  const response = await othent.initializeJWK(JWK_public_key_PEM);
  console.log(response);
} catch (error) {
  console.error(error);
}
```

_**JWKBackupTxn(JWT)**: Send a transaction with the specified JWK._

```javascript
// JWK backup transaction

const JWT = 'example_jwt';

try {
  const response = await othent.JWKBackupTxn(JWT);
  console.log(response);
} catch (error) {
  console.error(error);
}
```

### Contact

If you have any questions or issues with the SDK, please contact us at [hello@othent.io](mailto:hello@othent.io) or open an issue in the GitHub repository at [https://github.com/Othent](https://github.com/Othent/package).

### License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.
