---
description: 'Types of transactions: Contract internal writes  + Data uploading'
---

# 🌎 How it works

Othent uses Smartweave contracts and the Arweave blockchain for secure transactions and permanent data storage. Each user has their own unique contract accessed only by their unique JWT authentication, ensuring secure transactions between contracts.&#x20;

Data uploads to Arweave are verified through data hashes embedded in JWTs. Othent provides a simple and secure platform for transactions and data storage, prioritising user security and privacy.

### **The Current Authentication Method:**&#x20;

<figure><img src="../.gitbook/assets/Group 100.png" alt=""><figcaption></figcaption></figure>

Blockchains need private keys to ensure secure ownership and control over individual accounts and transactions. Private keys play a crucial role in cryptography-based systems by providing a means of authentication and digital signature.&#x20;

They are used to verify the identity of the owner and authorize transactions on the blockchain. Without private keys, anyone could falsely claim ownership of someone else's assets or manipulate transactions. By requiring private keys, blockchains maintain the integrity and security of the decentralized ledger, enabling individuals to securely manage their digital assets and participate in trustless transactions.

<figure><img src="../.gitbook/assets/Group 101 (1).png" alt=""><figcaption></figcaption></figure>

**Single private key:**

A single private key has certain negatives associated with it. Firstly, there is a lack of redundancy, meaning that if the single private key is lost or compromised, there is no backup or alternative to recover the associated cryptocurrency funds. Secondly, a single private key is vulnerable to theft. If the key is stolen or accessed by unauthorised individuals, they gain complete control over the associated cryptocurrency funds. Lastly, managing a single private key requires careful handling, as a simple mistake such as misplacing or forgetting the key can lead to permanent loss of access to the funds.

**Custodial private key:**

Custodial private keys have their own set of drawbacks. Users who entrust their private key to a custodian relinquish control over their funds, as they must rely on the custodian's policies and procedures. This limits their autonomy in managing their own cryptocurrency assets. Additionally, there are security risks involved with custodial private keys. Despite efforts by custodians to implement robust security measures, there is always a risk of hacking or internal breaches that could compromise the custodial private key and result in the loss of funds.

**MPC private key:**

MPC (Multi-Party Computation) private keys come with their own challenges. Firstly, there is added complexity compared to traditional single private keys. The setup and infrastructure required for MPC can be more intricate, making it harder for average users to understand and implement. Secondly, there is a potential for coordination failure. MPC relies on the cooperation of multiple parties to compute and manage the private key securely.&#x20;

Any failure or compromise in the MPC protocol or the participating parties could result in the loss or exposure of the private key and the associated funds. Lastly, MPC private keys may have a performance overhead, as they often require higher computational resources compared to single private keys, which can impact the speed and efficiency of transactions.

<figure><img src="../.gitbook/assets/Group 102.png" alt=""><figcaption></figcaption></figure>

### **Othent Smart Contract Transactions:**&#x20;

Othent utilizes smart contracts to enable secure and direct transactions between different contracts. Each user is assigned a unique smart contract that can only be accessed through a social login JSON Web Token (JWT). Here's an explanation of the key components and processes involved:

a. JSON Web Token (JWT): A JSON Web Token (JWT) is a compact and URL-safe means of representing claims between two parties. In Othent, a JWT serves as a secure authentication mechanism for accessing user-specific smart contracts. It is issued by the web2 platform upon successful social login and contains encoded information about the users desired transaction. A JWTs consist of three parts: header, payload, and signature. The header specifies the token type and signing algorithm, the payload contains the user-specific claims, and the signature ensures the integrity of the token. Othent then adds the users desired transaction metadata in the payload, thus allowing their contract to verify the users need.

b. User Smart Contracts: For each user, Othent deploys a unique smart contract. This contract is accessible only through the associated users JWT. The smart contract stores relevant user information such as their web2 ID and provides functionalities to facilitate contract to contract transactions. Users can interact with their respective contracts by signing transactions using their desired web2 service into a JWT.

c. Contract to Contract Transactions: With the use of their JWT, users can initiate transactions between different smart contracts. These transactions are executed securely and transparently, Othent ensures the integrity and authenticity of these transactions through RS256 JWTs.

### **Othent Data Transactions to Arweave:**&#x20;

Othent also supports data uploads to the Arweave blockchain, a decentralised storage network. This feature allows users to store data securely and retrieve it whenever needed. Here's an overview of the process:

a. Data Hashing: Before uploading data to Arweave, Othent generates a hash of the data. This hash acts as a unique identifier for the data and ensures its integrity. The hashing algorithm used by Othent follows industry best practices to generate secure and collision-resistant hashes.

b. JWT Integration: To establish a verifiable link between a user and the uploaded data, Othent embeds the data hash within the user's JWT. This inclusion ensures that the user has authorised the data upload and enables easy verification of the transaction.

c. Transaction Tagging: Othent includes the JWT, containing the data hash, as a tag within the Arweave transaction. This allows anyone with access to the transaction to validate that the user has signed off on the data upload. By combining the benefits of blockchain and cryptographic techniques, Othent enhances data integrity and transparency.

