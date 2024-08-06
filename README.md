---
description: Merging Web2 to Web3 user logins with a familiar and simple interface
---

# 👋 Welcome to Othent

<figure>
    <img src=".gitbook/assets/Group 104.png" alt="">
    <figcaption>Othent is pronounced OH-thent is a neologism of "OAuth" and "Authenticate".</figcaption>
</figure>

Othent is a service to manage Arweave custodial wallets backend by [Auth0](https://auth0.com/) and
[Google Key Management Service](https://cloud.google.com/kms/docs/key-management-service), enabling access to blockchain
networks using alternative methods beyond self-custodial private keys, making blockchain more widely accessible by
customizing the authentication process.

<figure>
    <img src=".gitbook/assets/Group 98.png" alt="">
    <figcaption>TODO: UPDATE</figcaption>
</figure>

Othent offers a powerful and user-friendly way for individuals and developers to access blockchain networks and create
web3 applications. With its design and seamless integration with existing Web2 technologies, Othent is targeting the
next evolution of blockchain and decentralized systems.

We leverage existing encryption and standards such as RS-256 and [JSON Web Tokens](https://jwt.io/), which are generated
by Auth0 using the users choice of traditional log in service, such as but not limited to:

- Google
- Twitter
- GitHub
- LinkedIn
- Microsoft
- Apple

We currently have support for 64 social connections, which is over 5B user log ins! Meaning over 5 billion people now
can easily have access to an Arweave web3 wallet with their existing credentials.

## 🥗 Othent's Features

<figure><img src=".gitbook/assets/Group 108.png" alt=""><figcaption></figcaption></figure>

**Existing private key wallets to onboard through social logins:**

Othent can be integrated by wallets and dApps to offer social logins and alternative authentications like API keys in
addition to self-custodial private keys. This can make the onboarding process smoother for users and enhance their
reach to Web2.

**Allow dApps to onboard through Web2:**

One of the biggest barriers to entry for many people when it comes to using dApps and interacting with the Web3
ecosystem in general is the complexity involved in setting up and managing a digital self-custodial wallet. However, by
allowing users to authenticate familiar Web2 mechanism that they are already familiar with (such as different social
media providers or email), it becomes much easier for them to start using dApps without needing to worry about the
technical details of setting up a wallet.

**Web2 apps as a channel to Web3 dApps and blockchains:**

By using Web2 apps as a channel to connect users to Web3 dApps and blockchains, we can help to bridge the gap between
the two worlds and make it easier for more people to start using decentralized applications. This can also help to
increase the overall adoption of blockchain technology and provide more opportunities for developers to create
innovative new dApps.

**Compatibility with the user, app, and blockchain:**

One of the key benefits of using a solution like Othent is that it is designed to be fully compatible with existing web2
applications and blockchain networks. This means that users can continue to use the same familiar tools and interfaces
that they are used to, without needing to learn a new set of skills or technologies.

Additionally, developers can easily integrate Othent into their existing applications without needing to make any major
changes or modifications to their code.

**Prevent losing private keys:**

By using Web2 authentication, your users don't need to fear losing their private keys or passphrase. If they forget
their password, they can simply reset it, just like they are used to.

## 👻 Othent's Missing and Upcoming Features

**Multiple addresses:**

Othent does not currently support creating and managing multiple private keys on the same account, or manually linking
different addresses to a specific account.

Right now, the only workaround around this is signing up using a different provider, which creates a different private
key and links the corresponding address to that new account.

**Importing and exporting private keys:**

Similarly, Othent doesn't currently support managing multiple private keys in any way not exposed in the API showcased
in these docs, including importing and exporting. 

Right now, the most similar thing to this is using [Arweave Wallet (arweave.app)](https://arweave.app) to watch a public
address, but you won't be able to transact using that wallet. Note ArConnect does not currently support watching public
addresses.

**Support for other blockchains:**

Othent currently supports only Arweave.

**Custom salt length for `sign()`:**

Othent doesn't support passing in a custom salt length.

**Custom encryption/decryption algorithm configuration:**

Currently, Othent only supports `RSA-OAEP` when using `encrypt()` and `decrypt()`.

**Public key encryption:**
  
Othent currently support symmetric encryption, using the currently authenticated user's AES-256 private keys. It does
not support asymmetric encryption using third party's public encryption RSAES keys, even thought it does use RSA for
signing.

**Public Key Directory (PDK):**

Othent doesn't offer a Public Key Directory (PDK), so if you need to verify third-party signatures, you'll have to get
the corresponding public keys from the original signer.

**Automatable money and smart contract wallets:**

Othent does not provide smart contract wallets, it's just a custodial wallet that manages the keys in behalf of its
users. Therefore, it doesn't currently support programmability oir transfer automation.

## 🌎 How does Othent work?

### **The Current Authentication Method:**&#x20;

Blockchains need private keys to ensure secure ownership and control over individual accounts and transactions. Private
keys play a crucial role in cryptography-based systems by providing a means of authentication and digital signature:

They are used to verify the identity of the owner and authorize transactions on the blockchain. Without private keys,
anyone could falsely claim ownership of someone else's assets or manipulate transactions. By requiring private keys,
blockchains maintain the integrity and security of the decentralized ledger, enabling individuals to securely manage
their digital assets and participate in trustless transactions.

<figure>
  <img src=".gitbook/assets/Group 100.png" alt="">
  <figcaption>TODO: Move to the first section</figcaption>
</figure>

Therefore, storing private keys securely and keeping them secret is critical to protect your assets and data.

> Othent uses Smartweave contracts and the Arweave blockchain for secure transactions and permanent data storage.Each user has their own unique contract accessed only by their unique JWT authentication, ensuring secure transactions between contracts.&#x20;
> 
> Data uploads to Arweave are verified through data hashes embedded in JWTs. Othent provides a simple and secure platform for transactions and data storage, prioritising user security and privacy.

<figure>
  <img src=".gitbook/assets/Group 101 (1).png" alt="">
  <figcaption></figcaption>
</figure>

**Single private key:**

A single private key has certain negatives associated with it. Firstly, there is a lack of redundancy, meaning that if the single private key is lost or compromised, there is no backup or alternative to recover the associated cryptocurrency funds. Secondly, a single private key is vulnerable to theft. If the key is stolen or accessed by unauthorised individuals, they gain complete control over the associated cryptocurrency funds. Lastly, managing a single private key requires careful handling, as a simple mistake such as misplacing or forgetting the key can lead to permanent loss of access to the funds.

**Custodial private key:**

Custodial private keys have their own set of drawbacks. Users who entrust their private key to a custodian relinquish control over their funds, as they must rely on the custodian's policies and procedures. This limits their autonomy in managing their own cryptocurrency assets. Additionally, there are security risks involved with custodial private keys. Despite efforts by custodians to implement robust security measures, there is always a risk of hacking or internal breaches that could compromise the custodial private key and result in the loss of funds.

**MPC private key:**

MPC (Multi-Party Computation) private keys come with their own challenges. Firstly, there is added complexity compared to traditional single private keys. The setup and infrastructure required for MPC can be more intricate, making it harder for average users to understand and implement. Secondly, there is a potential for coordination failure. MPC relies on the cooperation of multiple parties to compute and manage the private key securely.&#x20;

Any failure or compromise in the MPC protocol or the participating parties could result in the loss or exposure of the private key and the associated funds. Lastly, MPC private keys may have a performance overhead, as they often require higher computational resources compared to single private keys, which can impact the speed and efficiency of transactions.

<figure><img src=".gitbook/assets/Group 102.png" alt=""><figcaption></figcaption></figure>

> ### **Othent Smart Contract Transactions:**&#x20;
> 
> Othent utilizes smart contracts to enable secure and direct transactions between different contracts. Each user is assigned a unique smart contract that can only be accessed through a social login JSON Web Token (JWT). Here's an explanation of the key components and processes involved:
> 
> a. JSON Web Token (JWT): A JSON Web Token (JWT) is a compact and URL-safe means of representing claims between two parties. In Othent, a JWT serves as a secure authentication mechanism for accessing user-specific smart contracts. It is issued by the web2 platform upon successful social login and contains encoded information about the users desired transaction. A JWTs consist of three parts: header, payload, and signature. The header specifies the token type and signing algorithm, the payload contains the user-specific claims, and the signature ensures the integrity of the token. Othent then adds the users desired transaction metadata in the payload, thus allowing their contract to verify the users need.
> 
> b. User Smart Contracts: For each user, Othent deploys a unique smart contract. This contract is accessible only through the associated users JWT. The smart contract stores relevant user information such as their web2 ID and provides functionalities to facilitate contract to contract transactions. Users can interact with their respective contracts by signing transactions using their desired web2 service into a JWT.
> 
> c. Contract to Contract Transactions: With the use of their JWT, users can initiate transactions between different smart contracts. These transactions are executed securely and transparently, Othent ensures the integrity and authenticity of these transactions through RS256 JWTs.
> 
> ### **Othent Data Transactions to Arweave:**&#x20;
> 
> Othent also supports data uploads to the Arweave blockchain, a decentralised storage network. This feature allows users to store data securely and retrieve it whenever needed. Here's an overview of the process:
> 
> a. Data Hashing: Before uploading data to Arweave, Othent generates a hash of the data. This hash acts as a unique identifier for the data and ensures its integrity. The hashing algorithm used by Othent follows industry best practices to generate secure and collision-resistant hashes.
> 
> b. JWT Integration: To establish a verifiable link between a user and the uploaded data, Othent embeds the data hash within the user's JWT. This inclusion ensures that the user has authorised the data upload and enables easy verification of the transaction.
> 
> c. Transaction Tagging: Othent includes the JWT, containing the data hash, as a tag within the Arweave transaction. This allows anyone with access to the transaction to validate that the user has signed off on the data upload. By combining the benefits of blockchain and cryptographic techniques, Othent enhances data integrity and transparency.

## 🧑‍⚖️ License

The Othent Library is licensed under the MIT License. Please see the LICENSE file for more information.
