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

_Receives an object with your API ID called `API_ID`._

```javascript

// Initialise Othent

const othent = await Othent({ 
    API_ID: 'YOUR API ID'
})

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

#### queryWalletAddressTxns

Query a Othent users wallet addresses transactions

```javascript

// Query a users transactions

const walletAddress = 'Fqpw5BEnS1SCxwMJP4BhYCgzUmT8l3U6NNTBdjAXGF8'

const transactions = await othent.queryWalletAddressTxns({ walletAddress });

console.log(transactions);

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

#### verifyArweaveData

_Verify a Arweave transaction. Receives a Arweave transaction id._

```javascript

// Verify Bundlr transaction

const transactionId = 'Qi2K6IJY_VTlUJ3dszVm3Ot8UIOuMljMi8luw0ZdSnw'

const verifiedArweaveData = await othent.verifyArweaveData({ transactionId })

console.log(verifiedArweaveData)

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

#### verifyBundlrData

_Verify a Bundlr transaction. Receives a Bundlr transaction id._

```javascript

// Verify Bundlr transaction

const transactionId = 'VpyBrjsQ9jlKSYda17T8Dua1P-SpbWfJvGz2V-UPvfk'

const verifiedBundlrData = await othent.verifyBundlrData({ transactionId })

console.log(verifiedBundlrData)

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

_Backup an Othent account with a JWK private key. It receives a `{ privateKey }` object._

```javascript

// Initalize JWK to user

const privateKey = {
    "kty": "RSA",
    "e": "AQAB",
    "n": "iSGYBVYjH2jHL2ZfI3ymVWq-bqkPJUP3Zh8NzYrppU77RI-W_Gucg0ZMFHelgeY4xw2axhXWGJqLLFcp1Mr7xAZ3wIGLfiwvJNejFOwtJFcPbPoRKkTVLP0wWAZmbeKhnu1wFhfHrn2CYZEsVn2Z6BBUnXSo9CIG_Db55tfdcTM6gu6i9z_D3BUOhAeBeSKwqsc-G5KFG_r43I2tvVDpzWK8iUqTatRix0tvX1Mf1SLlovtEVBlNglmanTZdosZQyIxCS600ylCAaogWwYmh15PMz4Fw_pnkXpvTIGquOfVUoILxh7vbESsNknNKcrcD7uzrPyk7mBZeTDkjS-8avsTIDvibQGHznX_knAP2qiIHxjOmzp4jNRt7DphiIuXJZx5tm6kR7xOUcSiIxH4r0tiwWMiP95K1k7d9D8171CEn7YZmNJGYr4a-I8XML5vCq99SowksSoydi-UUN-hUNuiMLZKxi2EA_cI_DzX8WqzkLMHix6m8TQDRhUZ7otXiOXhloFWXV2KPiQD9WiioCcGUsGzUlRXxcpite5a3zLG8PoEaLSjZcFZrEd2CvMs44aCmb4JQyP54VE76ojo-Opy_0Yb8RMNKoX0QvUeD7NOK-hXBwIDBgm-QrDjgHQ6-RXs72cMiHjl2aib_YRwbwW68pg9G6C-iSM9MMwlbBv0",
    "d": "gIIi3J1kPMMMJrdg4PinR9TIsRttPhb7eZAQd1Z-rpPdlNqbO-H8wmjWUzfsulbtTlzJdmhwQo5RbjQg13GBjqog_x5ngs4VQAl0ot7RTwTnR9Dw1RO8UnTTISqeQsvnefA44ftW_YZQ8O4DBuqdmIP1R7lTu7VHpoQ-nL4enz7Kznij7-Cpw01YVRJTmxmPRfuBkIU2iIohPU7oSknRUM_-rwpcK_jsuKdQr5xOcIZLfPjLh6ROpqEh68JO7YO7oLUQS6r9lbrrHOp7qNM5_7Racvty0KWXBbIxoGdY7qehruoHPpQlL2mRRnUUh3xLC1SrAH27g0MzC2tgUIC6JiyV2BAdSGBu2ReRSu8TIL1UtxYBWpgsgggnMaGfqZbxREuU7mvFNYMtgR8juutswxOVEvDjmg9xyG-hFZ4vhVEq3VSGpSoZiFhqGeUIlGkBrgZzarjWFDvuNMSNdFLz7WXn2_XMNQkkco5BW5ZFsex_e06zc0c0-EJui8b4sLKoK7uHGlLN50HzM8HU-HnQGn-Zp-g0goi_-uiOtIq0KH2Zn-3XIZ1c8JWwkoi0-jl3VHtsbyaQKcjissRRiixtT5Rler4SFtaEtoNNojga0WVq0PGgAM1oQquhVTnKFlOepo3ryxK8gtUniUgbWKZZl79Bq5yCWG0Kq77fvqk_B2E",
    "p": "_rjPL7ak7zlmRGgEGIQOEbKKD6rNlkvsH0TrhuyTOAHLOoUVlnsJoAhLAThzy_7DypdOq7_uQfCc0QQkyjmYTdMHgsFx9HAzuYpL6BRaHrMPWKEu7ElmBbYHMNMSL3zWH8Ywufit1ttR6E62PHxcsOWkLFaJR6tqv5DmJ18ckhVfC8N7IaiEJVhMDcvZlARlcgInBpO4n35ff1XJr2HAEP3zBdn8Gy6VslbszHFyFAaoGRs_OxXlhEoxQnFtWVOnNjv1uL4WCI-HBCQLMqAVULIJ8UriXbImQL4CmkGS0pH7fFO1vqRyRreH3cEbKy514znMl6YOqBnlPhIcjNwJNw",
    "q": "idG9NXrUnQOJvOTbaUWGr9bVdK5Fauqu-Oey68W-77oXFbj_LwTM8K8LdQYcaZUShYs5PUxOVGvllm9K2mveYtqGC8N3FM9wSflxskpzrVI1SQednH_dv9EBtUdpriLW47IBZDWRp4TkoQAUUOU7GV3WlsDjq35ctIkoSRNsG3sYO6tKivdJWkANE7P6GY4uofy_NnMaTFsd3hzZx7ABJkDbLFLmtKN-Oipz29lKhaMTzaJJcTdJJVybREXrfeE426PGUNcnuWHY-uQz4APZHFtDMJCq7YBWVMEeazxEjPvcbxL8ky6EfhcXcRKnLApqFjFWyl6A1KZlunY4upi7aw",
    "dp": "H1Sh_09q2BXqU02r-0v64whf3O94XB04jNwQUEc3EHOACNGnxxuZInsCpsLH03ahpICZ55wy9R9gWoE0-T6-Ugw750Rd_N_0LMUq8v_V2eLSZ2dj-yJIDznFhqbfnMGxILVi9uz0jPHrEDTmS2hMimGkoON__TXDao6rEHqta_Z--1ZvBcPRhTpoGGZTe9ZSmARVwoRW-B82JdZqeUz_r9dclgKq9Lj1Jrt0Yu0tR_NNp9DnJSBbW7s4deC3v33_mjcj0TZoRWNKCyNX0UFJfeR4PpqkXzvzYpE8hra8FXRpR3CQcUOO3s3iQ09mRRhw3aMVXC3LrbeJr-nQYy8JXw",
    "dq": "ZE83-7jPDwkIM2gPGmv0P_-JlUdSVyNA_wEFBP4Ens8_BhyD_2DrGTMOj7pG68IInRJcMvVa_a8ah4exX5CraB_M-Lrn7UmeXPkle7McxsXS6riUStf2OiqRp7O2g3vwFAH3aUxkGx1qmpRINSji_u-BxG_YRXXPW8eIfseYI9hQJv3hX4vk479CxVh1bCxEXLptIeBc_75B2uv8xo6gB4uk-nnMWSW2Nfe4JAffaazsOPspoTGwF3VzvRl28UP_8j0dlrFCxHcnSlTWPPIQD8eM-8gP4JVMQJve3AYdjs-x_VZAZ4-v92YvNalx62gZFtYKaXinJB-IY1Kwr3-CyQ",
    "qi": "Oyu3BdOZhTCSru1wlwV6ep2Fw7hHUp5ZQkyGALGUcXhLP2BKVyykrpEgeBxrQMt429LfGpaJ95waXD9SG92OxJMJCE84OORxez5yEQPepACfvAffqMcxvUiXehXDdSQ_V-vx53Mo_OuJ3D4b83pGtt38fZvERcZzaR32NOLen_GSFyEJVi9uxpB_oDGVKAMIsKb_5aSVx1kGb-xT8sR9wPbH2y0cXJQrhI-gtQ6x5OctOs4gJY8ZJOYDqiCgxm7QJMZ70AayJjXVqvQrqNeuBVyM1urFsV5Q1lg_CjYrtBPmBPwJ6e0SuSr40zH0Hr-Xw0RvNRreZNpLDZ-ard27yg"
}
const transaction = await othent.initializeJWK({ privateKey })


console.log(transaction);

```

#### JWKBackupTxn

_Send a transaction with the specified JWK. It receives a `{ privateKey, sub, contract_id, tags, data, othentFunction }` object._

```javascript

// JWK backup transaction

const privateKey = {
    "kty": "RSA",
    "e": "AQAB",
    "n": "iSGYBVYjH2jHL2ZfI3ymVWq-bqkPJUP3Zh8NzYrppU77RI-W_Gucg0ZMFHelgeY4xw2axhXWGJqLLFcp1Mr7xAZ3wIGLfiwvJNejFOwtJFcPbPoRKkTVLP0wWAZmbeKhnu1wFhfHrn2CYZEsVn2Z6BBUnXSo9CIG_Db55tfdcTM6gu6i9z_D3BUOhAeBeSKwqsc-G5KFG_r43I2tvVDpzWK8iUqTatRix0tvX1Mf1SLlovtEVBlNglmanTZdosZQyIxCS600ylCAaogWwYmh15PMz4Fw_pnkXpvTIGquOfVUoILxh7vbESsNknNKcrcD7uzrPyk7mBZeTDkjS-8avsTIDvibQGHznX_knAP2qiIHxjOmzp4jNRt7DphiIuXJZx5tm6kR7xOUcSiIxH4r0tiwWMiP95K1k7d9D8171CEn7YZmNJGYr4a-I8XML5vCq99SowksSoydi-UUN-hUNuiMLZKxi2EA_cI_DzX8WqzkLMHix6m8TQDRhUZ7otXiOXhloFWXV2KPiQD9WiioCcGUsGzUlRXxcpite5a3zLG8PoEaLSjZcFZrEd2CvMs44aCmb4JQyP54VE76ojo-Opy_0Yb8RMNKoX0QvUeD7NOK-hXBwIDBgm-QrDjgHQ6-RXs72cMiHjl2aib_YRwbwW68pg9G6C-iSM9MMwlbBv0",
    "d": "gIIi3J1kPMMMJrdg4PinR9TIsRttPhb7eZAQd1Z-rpPdlNqbO-H8wmjWUzfsulbtTlzJdmhwQo5RbjQg13GBjqog_x5ngs4VQAl0ot7RTwTnR9Dw1RO8UnTTISqeQsvnefA44ftW_YZQ8O4DBuqdmIP1R7lTu7VHpoQ-nL4enz7Kznij7-Cpw01YVRJTmxmPRfuBkIU2iIohPU7oSknRUM_-rwpcK_jsuKdQr5xOcIZLfPjLh6ROpqEh68JO7YO7oLUQS6r9lbrrHOp7qNM5_7Racvty0KWXBbIxoGdY7qehruoHPpQlL2mRRnUUh3xLC1SrAH27g0MzC2tgUIC6JiyV2BAdSGBu2ReRSu8TIL1UtxYBWpgsgggnMaGfqZbxREuU7mvFNYMtgR8juutswxOVEvDjmg9xyG-hFZ4vhVEq3VSGpSoZiFhqGeUIlGkBrgZzarjWFDvuNMSNdFLz7WXn2_XMNQkkco5BW5ZFsex_e06zc0c0-EJui8b4sLKoK7uHGlLN50HzM8HU-HnQGn-Zp-g0goi_-uiOtIq0KH2Zn-3XIZ1c8JWwkoi0-jl3VHtsbyaQKcjissRRiixtT5Rler4SFtaEtoNNojga0WVq0PGgAM1oQquhVTnKFlOepo3ryxK8gtUniUgbWKZZl79Bq5yCWG0Kq77fvqk_B2E",
    "p": "_rjPL7ak7zlmRGgEGIQOEbKKD6rNlkvsH0TrhuyTOAHLOoUVlnsJoAhLAThzy_7DypdOq7_uQfCc0QQkyjmYTdMHgsFx9HAzuYpL6BRaHrMPWKEu7ElmBbYHMNMSL3zWH8Ywufit1ttR6E62PHxcsOWkLFaJR6tqv5DmJ18ckhVfC8N7IaiEJVhMDcvZlARlcgInBpO4n35ff1XJr2HAEP3zBdn8Gy6VslbszHFyFAaoGRs_OxXlhEoxQnFtWVOnNjv1uL4WCI-HBCQLMqAVULIJ8UriXbImQL4CmkGS0pH7fFO1vqRyRreH3cEbKy514znMl6YOqBnlPhIcjNwJNw",
    "q": "idG9NXrUnQOJvOTbaUWGr9bVdK5Fauqu-Oey68W-77oXFbj_LwTM8K8LdQYcaZUShYs5PUxOVGvllm9K2mveYtqGC8N3FM9wSflxskpzrVI1SQednH_dv9EBtUdpriLW47IBZDWRp4TkoQAUUOU7GV3WlsDjq35ctIkoSRNsG3sYO6tKivdJWkANE7P6GY4uofy_NnMaTFsd3hzZx7ABJkDbLFLmtKN-Oipz29lKhaMTzaJJcTdJJVybREXrfeE426PGUNcnuWHY-uQz4APZHFtDMJCq7YBWVMEeazxEjPvcbxL8ky6EfhcXcRKnLApqFjFWyl6A1KZlunY4upi7aw",
    "dp": "H1Sh_09q2BXqU02r-0v64whf3O94XB04jNwQUEc3EHOACNGnxxuZInsCpsLH03ahpICZ55wy9R9gWoE0-T6-Ugw750Rd_N_0LMUq8v_V2eLSZ2dj-yJIDznFhqbfnMGxILVi9uz0jPHrEDTmS2hMimGkoON__TXDao6rEHqta_Z--1ZvBcPRhTpoGGZTe9ZSmARVwoRW-B82JdZqeUz_r9dclgKq9Lj1Jrt0Yu0tR_NNp9DnJSBbW7s4deC3v33_mjcj0TZoRWNKCyNX0UFJfeR4PpqkXzvzYpE8hra8FXRpR3CQcUOO3s3iQ09mRRhw3aMVXC3LrbeJr-nQYy8JXw",
    "dq": "ZE83-7jPDwkIM2gPGmv0P_-JlUdSVyNA_wEFBP4Ens8_BhyD_2DrGTMOj7pG68IInRJcMvVa_a8ah4exX5CraB_M-Lrn7UmeXPkle7McxsXS6riUStf2OiqRp7O2g3vwFAH3aUxkGx1qmpRINSji_u-BxG_YRXXPW8eIfseYI9hQJv3hX4vk479CxVh1bCxEXLptIeBc_75B2uv8xo6gB4uk-nnMWSW2Nfe4JAffaazsOPspoTGwF3VzvRl28UP_8j0dlrFCxHcnSlTWPPIQD8eM-8gP4JVMQJve3AYdjs-x_VZAZ4-v92YvNalx62gZFtYKaXinJB-IY1Kwr3-CyQ",
    "qi": "Oyu3BdOZhTCSru1wlwV6ep2Fw7hHUp5ZQkyGALGUcXhLP2BKVyykrpEgeBxrQMt429LfGpaJ95waXD9SG92OxJMJCE84OORxez5yEQPepACfvAffqMcxvUiXehXDdSQ_V-vx53Mo_OuJ3D4b83pGtt38fZvERcZzaR32NOLen_GSFyEJVi9uxpB_oDGVKAMIsKb_5aSVx1kGb-xT8sR9wPbH2y0cXJQrhI-gtQ6x5OctOs4gJY8ZJOYDqiCgxm7QJMZ70AayJjXVqvQrqNeuBVyM1urFsV5Q1lg_CjYrtBPmBPwJ6e0SuSr40zH0Hr-Xw0RvNRreZNpLDZ-ard27yg"
  }
  
  const sub = 'google-oauth2|113378216876216346016'
  
  const contract_id = 'JUTWhO3PF_22ras6JVIlCALzqlkfscKBKPz7vxYKXA8'
  
  const tags = [ {name: 'Test', value: 'Tag'} ]
  
  const data = {
    toContractFunction: "createPost",
    toContractId: "tQKJCf2E9lIaNTjM8ELK6ATlJtef8cVmq68c9XnVuj0",
    txnData: {
      POST: "TEST POST!"
    }
  }
  const othentFunction = 'JWKBackupTxn'

  const transaction = await othent.JWKBackupTxn({ privateKey, sub, contract_id, tags, data, othentFunction })

  console.log(transaction)
  
```

#### encryptData

_Encrypt data with a secret key. It receives a `{ data, key }` object._

```javascript

// Encrypt data 

const data = 'I want this data encrypted!'

const key = 'password'

const encryptedData = await othent.encryptData({ data, key })

console.log(encryptedData)

```

#### decryptData

_Decrypt data with a secret key. It receives a `{ data, key }` object._

```javascript

// Decrypt data 

const data = 'U2FsdGVkX19sTWaZP0ST2zb7zvbTvvGU6lN0btbzGP3r13rSgZa8rgr4+XZG+yGX'

const key = 'password'

const decryptedData = await othent.decryptData({ data, key })

console.log(decryptedData)

```

#### deployWarpContract

_Deploy a SmartWeave Warp.cc contract. It receives a `{ contractSrc, state, tags }` object._

```javascript

// Deploy contract

const fetchContract = await fetch('https://othent.io/contract-new.js')
 
const contract = fetchContract.text()

const state = { testState: 'testState' }

const tags = [ { name: 'testTag', value: 'testTag' } ]

const deployedContract = await othent.deployWarpContract({ contractSrc, state, tags })

console.log(deployedContract)

```

## Contact

If you have any questions or issues with the SDK, please contact us at [hello@othent.io](mailto:hello@othent.io) or open an issue in the GitHub repository at [https://github.com/Othent](https://github.com/Othent/package).

## License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.
