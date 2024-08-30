---
description: Merging Web2 to Web3 user logins with a familiar and simple interface
---

# 👋 Welcome to Othent

<figure>
    <img src=".gitbook/assets/othent.png" alt="">
    <figcaption>Othent is pronounced OH-thent is a neologism of "OAuth" and "Authenticate".</figcaption>
</figure>

_Othent_ is a service to manage Arweave & ao wallets backend by [Auth0](https://auth0.com/) and
[Google Key Management Service](https://cloud.google.com/kms/docs/key-management-service), enabling access to blockchain
networks and making blockchain more widely accessible by customizing the authentication process.

_Othent_ offers a powerful and user-friendly way for individuals and developers to access blockchain networks and create
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
can easily have access to an Arweave & ao web3 wallet with their existing credentials.

## 🥗 Othent's Features

<figure>
  <img src=".gitbook/assets/web2-wallet.png" alt="">
  <figcaption>Examples of some of the social logins Othent supports.</figcaption>
</figure>

**Onboard through social logins:**

_Othent_ can be integrated by wallets and dApps to offer social logins. This can make the onboarding process smoother
for users and enhance their reach to Web2.

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

One of the key benefits of using a solution like _Othent_ is that it is designed to be fully compatible with existing web2
applications and blockchain networks. This means that users can continue to use the same familiar tools and interfaces
that they are used to, without needing to learn a new set of skills or technologies.

Additionally, developers can easily integrate _Othent_ into their existing applications without needing to make any major
changes or modifications to their code.

**Prevent losing private keys:**

By using Web2 authentication, your users don't need to fear losing their private keys or passphrase. If they forget
their password, they can simply reset it, just like they are used to.

## 👻 Othent's Missing and Upcoming Features

**Support for other blockchains:**

At the moment, _Othent_ is only available on [the Arweave network](https://www.arweave.org/) and [ao network](https://ao.arweave.dev/).

**Multiple addresses:**

_Othent_ does not currently support creating and managing multiple private keys on the same account, or manually linking
different addresses to a specific account.

Right now, the only workaround around this is signing up using a different provider, which creates a different private
key and links the corresponding address to that new account.

**Importing and exporting private keys:**

Similarly, _Othent_ doesn't currently support managing multiple private keys in any way not exposed in the API showcased
in these docs, including importing and exporting. 

Right now, the most similar thing to this is using [Arweave Wallet (arweave.app)](https://arweave.app) to watch a public
address, but you won't be able to transact using that wallet. Note ArConnect does not currently support watching public
addresses.

**Permission management**:

_Othent_'s permissions are hardcoded and cannot be changed.

{% hint style="danger" %}
**Caution:** Users using _Othent_ are giving dApps that use _Othent_ full control of their wallet , as discussed in
[`connect()`](./api/connect.md).
{% endhint %}

**Public key encryption:**
  
_Othent_ currently support symmetric encryption, using the currently authenticated user's AES-256 private keys. It does
not support asymmetric encryption using third party's public encryption RSAES keys, even thought it does use RSA for
signing.

**Public Key Directory (PKD):**

_Othent_ doesn't offer a Public Key Directory (PKD), so if you need to verify third-party signatures, you'll have to get
the corresponding public keys from the original signer.

**Subsidized transactions:**

Coming soon through [`@othent/pay`](https://www.npmjs.com/package/@othent/pay).

**Automatable money and smart contract wallets:**

_Othent_ does not provide smart contract wallets. Therefore, it doesn't currently support programmability or transfer
automation.

**Cryptographic algorithms limitations:**

- **Custom salt length for signing:** _Othent_ doesn't support passing in a custom salt length when calling `sign()`.

- **Custom encryption/decryption algorithm:** _Othent_ only supports `RSA-OAEP` when using `encrypt()` and `decrypt()`.

## 🌎 How does Othent work?

<figure>
  <img src=".gitbook/assets/key-pairs.png" alt="">
  <figcaption>Signing and verifying transactions using a private and public key, respectively.</figcaption>
</figure>

Blockchains need private keys to ensure secure ownership and control over individual accounts and transactions. Private
keys play a crucial role in cryptography-based systems by providing a means of authentication and digital signature,
while public keys are used to identify the owner and verify transactions and other cryptographic operations on the
blockchain.

For instance, to authorize and submit a transaction to, or permanently store data on the Arweave network, it first has
to be signed using the user's private key, and it can later be verified by other users using the signer's public key. 

Without private keys, anyone could falsely claim ownership of someone else's assets or manipulate transactions. By
requiring private keys, blockchains maintain the integrity and security of the decentralized ledger, enabling
individuals to securely manage their digital assets and participate in trustless transactions.

Therefore, storing private keys securely and keeping them secret is critical to protect your assets and data.

_Othent_ provides a simple and secure platform for transactions and data storage, prioritizing user security and privacy.

### Othent under the hood

<figure>
  <img src=".gitbook/assets/transaction-flow.png" alt="">
  <figcaption>Othent's transaction flow leveraging Google KMS and Auth0.</figcaption>
</figure>

_Othent_ creates an Arweave wallet (an address plus its corresponding public-private key pair) for every account, either
email-password or social login, and stores it in Google KMS.

When users wants to do any cryptographic operation with their keys (sign a transaction or encrypt/decrypt/hash some
data), they request an access token from Auth0, which contains a hash of the data to be used (the transaction or the
data to be encrypted/decrypted/hashed), and sends that, along with the data, to _Othent_'s API.

_Othent_'s API can then use Auth0's JWT token to authenticate the user and perform the operation they requested. That 
access token is then invalidated. This offers a tamper and reply proof system.

## 🥊 Othent vs Alternatives

<figure>
  <img src=".gitbook/assets/existing-key-storage-methods.png" alt="">
  <figcaption>Wallet types or key storage / custody methods.</figcaption>
</figure>

**Non-custodial / Self-custodial wallet (e.g. ArConnect):**

Non-custodial wallets / private keys has certain negatives associated with them:

- Firstly, there is a lack of redundancy, meaning that if the single private key is lost or compromised, there is no
  backup or alternative to recover the associated cryptocurrency funds.
  
- Secondly, a single private key is vulnerable to theft. If the key is stolen or accessed by unauthorised individuals,
  they gain complete control over the associated cryptocurrency funds.
  
- Lastly, managing a single private key requires careful handling, as a simple mistake such as misplacing or forgetting
  the key can lead to permanent loss of access to the funds.

**Othent:**

While Othent limits users autonomy in managing their own cryptocurrency assets, it also allows them to use traditional
authentication methods such as email and password, 2FA, social login, password/account recovery...
  
However, there are still security risks involved, and end users must secure their accounts and credentials properly.

**MPC wallet:**

MPC (Multi-Party Computation) wallets / private keys come with their own challenges:

- Firstly, there is added complexity compared to traditional single private keys. The setup and infrastructure required
  for MPC can be more intricate, making it harder for average users to understand and implement.

- Secondly, there is a potential for coordination failure. MPC relies on the cooperation of multiple parties to compute
  and manage the private key securely.

  Any failure or compromise in the MPC protocol or the participating parties could result in the loss or exposure of the
  private key and the associated funds.

- Lastly, MPC private keys may have a performance overhead, as they often require higher computational resources
  compared to single private keys, which can impact the speed and efficiency of transactions.

## 🧑‍⚖️ License

The _Othent_ Library is licensed under the MIT License. Please see the LICENSE file for more information.
