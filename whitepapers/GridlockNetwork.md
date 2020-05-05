# Gridlock Network

## A secure and private cryptocurrency storage service

devs@gridlock.network

V0.5 May 2020

### Abstract 

>Gridlock Network is a distributed keystore using a variety of network actors for increased security. Private keys are split into shares using the Threshold Signature Scheme (TSS), an m of n signature scheme, with a minimum recommendation of 3 of 5 shares for a rebuild threshold. Key shares are distributed to network actors for storage and transaction signing. The primary actor in the Gridlock Network is Enigma's Secret Network, which makes Gridlock a network of networks. Nodes on Enigma's network use Intel's trusted execution environments, called enclaves, to ensure secrecy of stored information. This insurance protects against collusion of participating nodes and increases availability due to share distribution across the entire Secret Network. Gridlock enhances this security and protects against side-channel attacks by distributing shares to non-Enigma actors to protect against the risk of broken enclaves. Additional actors include personal devices, trusted acquaintance devices, personal cloud devices and trusted key store services like Gridlock Watchlight.

## Overview

[Problem/Solution](#problem--solution)	

- Problem
- Solution

[Gridlock Architecture](#Gridlock Architecture)

- Overview	
- Additional Actors
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

Cryptocurrency users only two options when storing assets, either with a third-party cryptocurrency exchange or a personal cryptocurrency wallet. Both options have drawbacks, in privacy, usability, and security, some of which can ultimately lead to a loss of all assets.

Exchanges are centralized entities with complete control over a user’s funds and knowledge of user's identities.  User are subject to arbitrary transaction delays and withheld assets based on the whim's of the exchange. Furthermore, all assets are lost if an exchange is hacked, goes out of business, exit scams or is otherwise shut down. Many exchanges have shut down in one of these ways, which has led to the saying “Not your keys, not your coins”. The saying promotes storing of assets in personal wallets outside the oversight of exchanges.

However, while crypto wallets give control back to the user, that control is a double-edged sword. Full control means a user is responsible for the management and security of their private keys. All assets vanish if a private key is lost or stolen. Most wallets do have backup mechanisms- namely mnemonic phrases - which allow users to recover lost keys. The problem here is that the backup itself is still a single point of failure. If a user's mnemonic phrase is stolen, all assets are lost. 

Other solutions like hardware wallets, smart contract wallets, or multi-sig wallets add value in one way or another but all still have problems with security and usability. A solution is needed that doesn't sacrifice privacy in the name of usability or usability in the name of security. 



### Solution

Gridlock overcomes problems with security, usability, and privacy by distributing a user's private keys across multiple devices. 

Keys are split into key shares using a Threshold Signature Scheme,  which requires a designated threshold of shares before the key is usable. The initial recommended threshold is `3 of 5` meaning that five key shares are distributed, and three must come together to rebuild the key.  Shares are distributed among participating network actors for storage. 

The primary actor is Enigma's Secret Network, making Gridlock a network of networks. Enigma's network ensures the secrecy of shares by mandating that nodes running the network use Intel trusted execution environments (TEE), enclaves, for all computations and data storage. This feature encrypts all sensitive data, so it is hidden from everyone, including the node operator. This restriction allows for the availability benefits of multiple storage nodes and protects against the possibility of malicious node operators.

Enigma enclaves are potentially susceptible to side-channel attacks which can allow hackers or node operators to break the security of an enclave. The viability of these attacks is questionable outside an academic setting given a correctly hardened protocol. Still, the potential of loss is too great to rely solely on an enclave to ensure the security of a private key. For additional security, secondary non-Enigma actors are necessary. 

Secondary network actors provide insurance against the possibility of cracked enclaves in Enigma's network. Additional actors include personal devices, trusted acquaintance devices, personal cloud devices and trusted key store services like Gridlock Watchlight. The variety of each actor increases network security by varying the attack surface, so a flaw in any area of the network does not cause a loss of assets. 

Gridlock wallets are highly usable since users are not required to manage their private keys. Instead, keys are distributed throughout the network, controlled by the user alone. To  access a wallet, owners provide a hashed identity and credentials. User identities are hashed and encrypted before storage which means no network actor knows the identity of the wallet owner. 



## Gridlock Architecture

### Primary Actor

Enigma privacy-preserving network is used to store one or more key shares as long as the network does not control a majority of shares. This actor allows Gridlock to use the strength of a privacy-preserving network while removing the risk of problems with a compromised network.

### Additional Actors

##### Personal Device

Gridlock utilizes a client-side application for wallet generation and usage. The application can encrypt and store one key share on the device. Users can add more actors of the same type with additional personal devices or hardware-based key storage devices. 

##### Personal Cloud Device

Microservers and microservices allow users to store personal data on a cloud server. These servers are affordable, always online, and always in the owner's control. Gridlock aims to work with cloud providers to make the creation of these devices as easy as a click of a button. 

##### Acquaintance device

One or more trusted acquaintances can store a key share using the client-side application with minimal effort. The storage and use of a share do not require any input from the acquaintance beyond the initial acceptance. For transaction signing, the device must be online to provide their share of the signature; therefore the use of acquaintance devices is limited to half of the total participating devices, m-1, to ensure constant availability. 

##### Trusted service

A trusted key store service, like Gridlock Watchlight, can store a key share and provide additional protection not available in other "passive" storage options. This option adds benefits of modern FinTech security practices, like suspicious transactions, without the ultimate control of a full key store service. 



### Key Generation

Distributed key generation ensures that the private keys are never fully available which eliminates problems with potentially compromised nodes. TSS requires multiple rounds of communication between participating actors to generate a private key, the amount of communication required depends on the number of participants. 

Prior to user interaction, private-public keypairs are generated for all supported coins, reducing the wallet generation time for new users. Keys are stored in the system and available for user association once a user account is created. 



## User Experience



### Wallet Generation

New users generate wallets for asset storage by associating their access information and distributed keys in the network. Users create define a identity and access credentials as a means to access their wallet. Both the identity and credentials are salted with the name of the target actor (e.g. Enigma) and hashed. Hashing a user's identity increases privacy while the hashing of access information reduces the possibility of cross-actor impersonation attacks. Users can begin storing assets in their new distributed keystore after wallet association is confirmed. 



### Signing

To transfer funds our of the network or sign transactions, users must authenticate with each network actor and request the actor's portion of the signature. The user starts by sending a packet of information containing their hashed identity and hashed credentials to a network participant. They also include the same information encrypted with public keys of other participants. This first node contacted becomes the 'primary actor' and is responsible for communication between other participants to generate a fully signed transaction. They are also responsible for communicating the signed transaction to the associated blockchain. 

### Account Recovery

Traditional account recovery mechanisms often require that users give up their privacy and autonomy to a central authority. Gridlock Network represents everything that the traditional world isn't. 

That said, maintaining user privacy and autonomy in a decentralized system is difficult since there is no central authority to fall back on. Gridlock Network solved this problem by introducing the concept of *fading security*. Fading security is the process in which the credentials required to access a wallet are systematically reduced until access is reestablished. If a user is not able to authenticate with their wallet, they can wait until they are able to meet a subset of all security requirements. 

The specifics of the fading security engine are complex and cannot be fully refined until tested in real-world scenarios. However, the basic reduction of security requirements would trigger in a way such that it reduces the vulnerabilities of various attack vectors ranging from physical attack, remote attack, and collusion attacks. 



## Advanced Features

### Multi-sig Accounts

Multi-signature accounts are as simple as supporting two or more identities with the same wallet. Once added, future transaction require a defined subset of identities before a transaction is signed. The default is `n of n` identities but can be changed if approved by all parties.   This provides all the benefits of multi-sig authorizations without the weight of heavy multi-sig signatures on the blockchain. Since the approval logic is off-chain, the user can define granular logic beyond the standard yes-no logic in a multi-sig wallet. 

Wallets can also store internal metadata to document the identities that authorized each transaction. This retains the auditability of each transaction but keep privacy by restricting that information to authorized users. 

### One-way asset flow

A public key is necessary when receive

Periodic rotating of private keys is important to increase system security. This reduces the time-window in which an attacker can obtain a private key. The attacker has to compromise each share holder before the private key is changed. TSS-based wallets have the ability to rotate key shares such that a new private key is created but the public-key remains unchanged. This is useful when the public key is needed for long term use but typically the user is not concern with how keys are used.

It is therefor possible to have a public key for receiving funds only and a separate public key for sending funds. Put another way, all funds entering the system do not necessarily need to stay associated with their initial public key. The funds can rotate through the network as long as the user is able to track and spend funds when desired. This has enormous privacy benefits as the system because a mixer by default. 

### Asset Management

Gridlock Network is effectively non-custodial since no entity has control of stored funds. The only person able to access and control funds is the owner. However, the system can include include a permission framework that allows for granular permissions. Asset owners can define which services have access to funds and for what reason. For example, the owner can determine which services have access for investment purposes. This allows for a marketplace of services that benefit the both the user and service provider. 

### Watchlight Service

Gridlock Watchlight is an additional service that can add oversight protection for wallet owners. The service does not have ultimate control of a user's funds, but rather it is closely connected to the wallet and can monitor activity. This adds the benefit of professional monitoring which can suspicious transactions or coordinated attacks which are not normally identifiable in a randomly distributed system. If suspicious activity is identified, that service can proactively notify the owner. The service can tread the line between privacy and proactive monitoring. 



## Conclusion

Gridlock Network is the first truly secure and private cryptocurrency storage solution. Threshold Signatures combined with Trusted Execution Environments provide unparalleled security and availability, beyond any other solution available today. The offloading of complex key management eliminates one of the biggest barriers to mainstream crypto adoption. The elimination of a central authority vastly increases security and maintains a user's privacy. 
