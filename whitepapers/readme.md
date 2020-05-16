# Gridlock Network

## A secure and private cryptocurrency storage service

[devs@gridlock.net](mailto:devs@gridlock.net)work

V0.6 May 2020

### Abstract 

Gridlock Network is a distributed keystore using a variety of network devices for increased security. Private keys are split into shares using the Threshold Signature Scheme (TSS), an m of n signature scheme, with a minimum recommendation of 3 of 5 shares for a rebuild threshold. Key shares are distributed to network devices for storage and transaction signing. The primary device in the Gridlock Network is Enigma's Secret Network, which makes Gridlock a network of networks. Nodes on the Secret Network use Intel's trusted execution environments, called enclaves, to ensure secrecy of stored information. This insurance protects against collusion of participating nodes and increases availability due to share distribution across the entire Secret Network. Gridlock enhances this security and protects against side-channel attacks by distributing shares to non-Enigma devices to protect against the risk of broken enclaves. Additional devices include personal devices, trusted acquaintance devices, personal cloud devices,
and trusted key store services like Gridlock Watchlight.

## Overview

[Problem/Solution](#problem--solution) 

- Problem
- Solution

[Network Architecture](#network-architecture)

- Overview 
- Additional devices
- Key Generation

[User Experience](#user-experience) 

- Wallet Generation
- Signing
- Account Recovery

[Advanced Features](#advanced-features)

- Multi-sig Accounts 
- One-way Asset Flow
- Asset Management
- Watchlight Service

[Conclusion](#conclusion) 

## Problem / Solution

### Problem

Cryptocurrency users have only two options when storing assets, either with a third-party cryptocurrency exchange or a personal cryptocurrency wallet. Both options have drawbacks in privacy, usability, and security, some of which can ultimately lead to a loss of all assets.

Exchanges are centralized entities with complete control over a user's funds and knowledge of the user's identities. Users are subject to arbitrary transaction delays and withheld assets based on the whim of the exchange. Furthermore, all assets are lost if an exchange is hacked, goes out of business, exit scams, or is otherwise shut down. Many exchanges have shut down in one of these ways, which has led to the saying "Not your keys, not your coins". The saying promotes storing of assets in personal wallets outside the oversight of exchanges.

While crypto wallets give control back to the user, that control is a double-edged sword. Full control means a user is solely responsible for the management and security of their private keys. All assets vanish if a private key is lost or stolen. Most wallets do have backup mechanisms, namely mnemonic phrases, which allow users to recover lost keys. The problem here is the backup itself is still a single point of failure. If a user's mnemonic phrase is lost or stolen, all assets are unrecoverable. 

Other solutions like hardware wallets, smart contract wallets, or multi-sig wallets add value in one way or another, but all still have problems with security and usability. The community needs a solution that doesn't sacrifice privacy in the name of usability or usability in the name of security. 

### Solution

Gridlock overcomes problems with security, usability, and privacy by distributing a user's private keys across multiple devices. 

Keys are split into key shares using a Threshold Signature Scheme, which requires a designated threshold of shares before the key is used. The initially recommended threshold is 3 of 5, meaning that 5 key shares are distributed, and 3 must come together to rebuild the key. Shares are distributed among participating network devices for storage. 

The primary tool for key storage is Enigma's Secret Network, making Gridlock a network of networks. Enigma's network ensures the secrecy of shares by mandating that nodes running the network use Intel’s trusted execution environments (TEE), also known as enclaves, for all computations and data storage. This feature encrypts all sensitive data, hiding it from everyone, including the node operator. This restriction allows for the availability benefits of multiple storage nodes and protects against the possibility of malicious node operators.

Enigma enclaves are potentially susceptible to side-channel attacks which can allow hackers or node operators to break the security of an enclave. The viability of these attacks is questionable outside an academic setting, given an appropriately coded protocol. Still, the potential of loss is too great to rely solely on an enclave to ensure the security of a private key. For additional security, secondary non-Enigma devices are necessary. 

Secondary network devices provide insurance against the possibility of cracked enclaves in Enigma's network. Additional devices include personal devices, trusted acquaintance devices, personal cloud devices, and trusted key store services like Gridlock Watchlight. The variety of each device increases network security by varying the attack surface, so a flaw in any area of the network does not cause a loss of assets. 

Gridlock wallets are highly usable since users are not required to manage their private keys. Instead, keys are distributed throughout the network, controlled by the user alone. To access a wallet, owners provide a hashed identity and credentials. User identities are hashed and encrypted before storage which means no network device knows the identity of the wallet owner. 

## Network Architecture

Key shares are distributed across multiple devices to gain the security benefits of each. The [key share topology document ](https://github.com/GridlockNetwork/Resources/blob/master/documentation/Gridlock%20-%20Key%20Distribution%20Topology.pdf)shows a default 3-of-5 key share distribution. 

### Primary device(s)

Enigma's privacy-preserving network is the primary share store option in Gridlock's network due to its high availability and usage of secure SGX enclaves. We plan to use this network to store multiple key shares, as long as the network does not control a majority of shares. This strategy allows Gridlock to leverage the strength of a privacy-preserving network while removing the risks associated with compromised SGX enclaves.

### Additional devices

##### Personal Device

Gridlock uses a client-side application for wallet generation and usage. The application is also a storage participant and can encrypt and store a share of the private key. Users can add more devices of the same type with additional personal devices or hardware-based key storage devices. 

##### Personal Cloud Device

Microservers and microservices allow users to store personal data on a cloud server. These servers are affordable, always online, and always in the owner's control. Gridlock aims to work with cloud providers to make the creation of these devices as easy as a click of a button. 

##### Acquaintance device

One or more trusted acquaintances can store a key share using the client-side application with minimal effort. The storage and use of a share do not require any input from the acquaintance beyond the initial acceptance. For transaction signing, the device must be online to provide their share of the signature; therefore the use of acquaintance devices is limited to half of the total participating devices, m-1, to ensure constant availability. 

##### Trusted service

A trusted key store service, like Gridlock Watchlight, can store a key share and provide additional protection not available in other "passive" storage options. This option adds benefits of modern FinTech security practices, like suspicious transactions, without the ultimate control of a full key store service. 

## User Experience

### Wallet Generation

New users generate a Gridlock wallet by creating an "account" with Gridlock and defining an identity and log-in credentials. The identity consists of non-private information, such as full name and government ID, and access credentials, which are a combination of password, 2FA, biometrics, etc. This information is required so decentralized devices can uniquely identify the user. All information is encrypted client-side, so the identity of the user remains secret. 

Once the user has created a wallet, they can generate addresses for each cryptocurrency they wish to store. 

### Funds Transfer and Transaction Signing

Users transfer funds into the network by sending their assets to the crypto addresses provided by Gridlock.

To transfer funds out of the network or sign transactions, users must authenticate with each network device and request the device's portion of the signature. However, this work is done without user interaction. All the user has to do is confirm their identity and access credentials and transmit that information along with the transaction they wish to perform. 

### Account Recovery

Traditional account recovery mechanisms often require that users give up their privacy and autonomy to a central authority. Gridlock Network aims to solve that problem with the first truly decentralized system.

However, there are struggles with this goal, particularly when it comes to account recovery. Since there is no central authority to fall back on, we must consider how to best walk the line between security and usability. We feel we've solved this problem by introducing the concept of *fading security*. 

Fading security is the process in which the credentials required to access a wallet are systematically reduced until access is re-established. If something goes wrong and a user cannot access their wallet, they only have to wait until the fading security mechanism catches up to a point where they can re-establish access. This can be inconvenient at times, but we feel this is an easy trade-off to gain perfect security and complete control.

## Technical Process flow

### Wallet Generation

The user provides multiple pieces of identification information (i1, i2... in), such as name and a government ID, and credential information (c1, c2... cn), such as password and either a 2FA or a biometric key. Using the provided information, Gridlock will construct a custom Merkle tree combining each element. This allows us to generate password tiers used by the fading security engine (see below). 

Prior to transmittal, each data element is hashed client-side using Argon2d with a moderately large number of iterations. The assumption is that crypto transactions are not extremely common, so a multi-second wait is a fair trade-off for increased protection against brute-force attacks. Additionally, the finality time of many blockchains makes the extended client-side delay negligible (i.e. a three-second wait for a Bitcoin transaction, which takes an average of 10 minutes to finalize). 

We will create n sets of hashed credentials for each participating device to create unique hashed sets for each participant. Aragon2 automatically provides a unique salt per hash. This allows us to protect against user impersonation between devices. In other words, the H(c1) on one device will not match H(c1) on another device. Compromised devices cannot coerce additional key shares using their hashed credentials. 

### Key Generation

Distributed key generation ensures that the private keys are never fully available, which eliminates problems with potentially compromised nodes. TSS requires multiple rounds of communication between participating devices to generate a private key; the amount of communication required depends on the number of participants. 

Before user interaction, private-public keypairs are generated for all supported coins, reducing the wallet generation time for new users. Keys are stored in the system and available for user association once a user account is created. 

### Transaction Signing

There are two proposed states for transaction signing based on the maturity of the network. The first state incorporates a central communication hub, which significantly reduces many parts of the architecture. 

Note: The decision to include a central point of communication was not made lightly as it goes against the ethos of the blockchain community. With the understanding that a central communication-only hub *does not affect the security of the product*, we decided to incorporate this in the initial release while we stabilize the rest of the network. 

<img src="https://github.com/GridlockNetwork/Resources/blob/master/images/Key%20Signing%20Architecture%20-%20phase1.png">

With this architecture, funds transfer and transaction signing occur as follows:

1) The user transmits one packet of transaction information to the communication hub for each participating storage device. Each packet contains the user's identity, credentials, and transactiom information and is encrypted with the public key of the target storage device. The communication hub cannot access the contents of the packet and exists only to forward to the target storage device.

2) Each storage device validates the user's credentials. If accepted, it returns their portion of the signed transaction back to the communication hub. 

3) The communication hub combines all signature pieces and transmits the complete signed transaction to the correct blockchain network. 


The second state is much like the first, except it eliminates the communication hub. 

<img src="https://github.com/GridlockNetwork/Resources/blob/master/images/Key%20Signing%20Architecture%20-%20phase2.png">

With this architecture, funds transfer and transaction signing occur as follows:

1) The user transmits one packet of transactiom information for each participating storage device to *any* participating storage device. The first contacted device becomes the 'primary device' and is responsible for communication between other participants, as well as transaction signing. The primary device forwards transaction packets to their designated participants. 

2) Each storage device validates the user's credentials. If accepted, it returns their portion of the signed transaction back to the primary device. 

3) The primary device combines all signature pieces and transmits the complete signed transaction to the correct blockchain network. 

### Fading Security

Fading security ensures guaranteed access to the user's wallet without centralized oversight. This is possible by reducing the requirements for access after a pre-determined time window has elapsed without the user making a connection. 

The following example shows how the security engine might reduce access requirements based on an arbitrary number of security elements or "checks". The system is designed to give precedence to stronger access credentials.

<code>G</code> = **G**uardians		 	 <code>D</code> = **D**evice (2FA)	            <code>P</code> = **P**assword

<code>B</code> = **B**iometric key		<code>A</code> = Sum of **A**ny checks	<code>C</code> = Total number of **C**hecks

<code>T</code> = number of **T**ime windows elapsed without access

The engine iterates through the defined logic whenever a user requests access. The system starts at a time window <code>T</code> of 0 and increments by 1 for each time new window without a successful connection. Once a connection is established, <code>t</code> is reset to 0. 

**Tier 1 :** If <code>C</code> - <code>T</code> - 2 = 0 -> evaluate credentials and grant access if <code>C</code> - <code>T</code> - 2 = <code>B</code> + <code>P</code> + <code>A</code>

**Tier 2:** If <code>C</code> - <code>T</code> - 1 = 0 -> evaluate credentials and grant access if <code>C</code> - <code>T</code> - 1 = (<code>B</code> or <code>P</code>) + <code>A</code>

**Tier 3:** If <code>C</code> - <code>T</code> = 0 -> evaluate credentials and grant access if <code>C</code> - <code>T</code> = <code>A</code> AND <code>A</code> > 0

**Tier 3a:** If  <code>C</code> - <code>T</code> = 0 AND <code>A</code> > 0  -> grant access if based on user identity only as long as the requestor put up ~$1 worth of cryptocurrency as collateral. This helps stop network "scanning" looking for open accounts.

**Tier 5:** Transfer funds to pre-defined Guardian

## Advanced Features

### Multi-signature Accounts

Multi-signature accounts are as simple as supporting two or more identities with the same wallet. Once added, future transactions require a defined subset of identities before a transaction is signed. The default is `n of n` identities but can be changed if approved by all parties. This option provides all the benefits of multi-sign authorizations without the weight of heavy multi-sig signatures on the blockchain. Since the approval logic is off-chain, the user can define granular logic beyond the standard yes-no logic in a multi-sig wallet. 

Wallets can also store metadata to document the identities that authorized each transaction. The information is stored within the wallet. This information allows users to keep an audit trail while maintaining on-chain privacy. 

### One-way asset flow

Periodic rotating of private keys is important to increase system security. This rotation reduces the time-window in which an attacker can obtain a private key. An attacker must compromise each device, storing a key share before the private key is changed. TSS-based wallets can rotate key shares to generate a different set of key shares while retaining the original public key. This mechanism is useful when users want to retain the public key for long-term use, but the typical user does not require this benefit.

It is, therefore, possible to have a public key for receiving funds only and a separate public key for sending funds. Put another way, all funds entering the system are not restricted to the public key used to import funds. Gridlock can freely rotate funds throughout the network as long as the user can track and transfer funds when desired. This rotation has enormous privacy benefits as the system becomes a mixer by default. 

### Asset Management

Gridlock Network is effectively non-custodial since no entity has control of stored funds. The only person able to access and control the funds is the owner. However, the system can include a permissions framework that allows for assignment of granular permissions to specified services. Asset owners can define which services have access to funds and for what reason. For example, the owner can determine which services have access for investment purposes. This granular level of control allows for a marketplace of services that benefit both the user and the service provider. The inclusion of explicit permissions helps assuage consumer fears when considering new services. 

### Watchlight Service

Gridlock Watchlight is an optional add-on service that provides oversight protection for wallet owners. The service does not have the ultimate control of a user’s funds. Instead, it can closely monitor connected wallets and activity. This key share storage service adds the benefit of professional monitoring, which watches for suspicious transactions or coordinated attacks. This type of oversight is difficult with the standard distributed devices. If Watchlight identifies any suspicious activity, we can proactively notify the owner. This service bridges the gap between privacy and proactive monitoring. 

## Conclusion

Gridlock Network is the first truly secure and private cryptocurrency storage solution. Threshold Signatures combined with Trusted Execution Environments provide unparalleled security and availability, beyond any other solution available today. The offloading of complex key management eliminates one of the biggest barriers to mainstream crypto adoption. The elimination of a central authority vastly increases security and maintains a user’s privacy. 
