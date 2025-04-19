---
icon: square-small
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Smart Contracts

A **smart contract** is essentially a computer program that runs on the blockchain. What makes it special is that this program follows a set of predefined rules and, once certain conditions are met, it executes automatically, without the need for anyone to supervise it.

To understand it more simply, think of a smart contract as a **vending machine**. You insert a certain amount of money, select what you want to buy, and the machine delivers the product. The entire process occurs without anyone having to intervene. The smart contract works similarly - if the conditions are met (like inserting the correct amount of money), it automatically executes what it's programmed to do (in this case, deliver the product).

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

### How does it work?

In the Ethereum network, smart contracts are the engine of **dApps** (decentralized applications) and allow anyone to create rules and enforce them automatically. These contracts are written in a programming language called **Solidity**, which was specifically designed for creating smart contracts on Ethereum.

Once the contract is written, it is deployed on the blockchain and becomes immutable. This means that once it's on the blockchain, **no one can change or manipulate it**. Any transaction that interacts with that contract will follow the rules that were established from the beginning.

For example, imagine a smart contract that says: "if John sends 5 AVAX to this contract, then the contract will send him an NFT". Once John sends the 5 AVAX, the contract will automatically send him the NFT, without any person having to intervene to verify or approve the transaction. This is what makes smart contracts so powerful - they eliminate the need for intermediaries and work completely automatically.

### Risks

Although smart contracts offer enormous potential, they are not perfect. Being based on code, **an error in the code can have serious consequences**. A famous example is the **DAO hack** in 2016, where an error in the smart contract allowed an attacker to drain millions of dollars from the organization.

This incident made it clear that while smart contracts eliminate intermediaries, they also introduce new risks - if the code is not secure, it can be exploited. That's why it's crucial that contracts are audited and reviewed before being deployed on the blockchain.

### Smart contracts in other networks

Although Ethereum was the first network to popularize smart contracts, it's not the only one that uses them. Other blockchains like **Avalanche**, **Binance Smart Chain**, **Starknet**, and **Solana** also allow the use of smart contracts. In fact, many of these networks are compatible with the **EVM** (Ethereum Virtual Machine), which means that smart contracts written for Ethereum can be executed on other platforms with little additional effort.
