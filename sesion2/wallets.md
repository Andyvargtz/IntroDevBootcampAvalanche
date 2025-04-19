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

# Wallets

Now that we have a brief context about how we interact with the blockchain through cryptographic keys, the next natural step is to talk about wallets. These tools play a very important role in managing and protecting our cryptocurrencies and digital assets, acting as the interface between users and the blockchain. But what exactly is a wallet and how does it work?

### What is a Wallet?

Despite its name, a wallet (**digital wallet**) does not store cryptocurrencies in the same way that a physical wallet stores money. Instead of having the assets directly, the wallet stores the private key that allows you to access your cryptocurrencies on the blockchain. Every time you make a transaction, your wallet uses this key to sign and authorize the movement of assets.

In fact, cryptocurrencies are not "stored" in the wallet as such, but rather reside on the blockchain. What the wallet does is allow you to access those cryptocurrencies associated with a **public key** by using the corresponding **private key**. That is, the wallet acts as a remote control that allows you to manage your funds that are always on the blockchain.

### Types of Wallets

There are several types of wallets, each with different levels of security and accessibility, allowing users to choose the one that best suits their needs. These are the most common types:

1. **Software Wallets:** Also known as **hot wallets**, they are applications that you install on your computer or phone. These wallets are accessible and convenient, allowing you to make transactions from anywhere where you have internet access. The most popular examples include **MetaMask**, **Trust Wallet**, and **Core**.
2. **Hardware Wallets:** Also known as **cold wallets**, they are physical devices, such as **Ledger** or **Trezor**, that store private keys offline. These are considered one of the most secure forms of cryptocurrency storage because they keep your keys out of reach of the internet, protecting them from possible hacks.
3. **Paper Wallets:** This is a completely offline way to store private and public keys. These are simply physical prints containing the private key and public key in alphanumeric or QR format. If generated correctly, these wallets have no digital connection, making them immune to online hacks.
4. **Custodial Wallets:** This is one where a third party, generally an exchange platform like **Binance** or **Coinbase**, stores your private keys on your behalf. This means you trust said entity to custody and protect your funds.

### How do Wallets Work?

The operation of a wallet is based on the use of **cryptographic keys**. When you generate a wallet, a pair of **private key** and **public key** is created. As we already explained, the private key is what allows access to your funds, while the public key is like an address that you can share to receive payments.

Every time you send cryptocurrencies, the wallet uses the private key to **sign** the transaction digitally. This process confirms that you are the owner of the funds and authorizes their transfer. After signing, the transaction is transmitted to the blockchain network where **nodes** validate it and record it in the next block.

In wallets like **MetaMask** and **Core**, private keys and the seed phrase are managed locally on the user's device, which means you have complete control over your funds, but you also bear the responsibility of protecting the private keys.

### Opening your Core Wallet

Core is a blockchain platform developed by **Avalanche**, which allows users to interact with the Avalanche network and other **EVM** (Ethereum Virtual Machine) compatible blockchains in an efficient and secure manner. It is important that you learn how to obtain and configure your **Core** wallet so you can start interacting with the Avalanche ecosystem.

1. **Download Core:** You can download the web extension or the official **Core** application:

{% embed url="https://chromewebstore.google.com/detail/core-crypto-wallet-nft-ex/agoakfejjabomempkjlepdflaleeobhb" %}

{% embed url="https://core.app/es/?downloadCoreMobile=1" %}

2. **Create a new wallet:** Once you have installed the extension or the **Core** application, follow these steps to create your wallet:
   * Open the application or extension and select the option **"Create new wallet"**.
   * Core will generate a **seed phrase** of 24 words for you. This phrase is essential for recovering your wallet if you lose access to your device, so make sure to write it down in a safe place and do not share it with anyone.
   * Confirm the seed phrase in the next step, you will be asked to select some words in the correct order to verify that you have saved it correctly.
3. **Configure your wallet:** After creating your wallet, Core will ask you to set a **password**. This password is necessary to access your wallet on your device and perform transactions.
4. **Connect with Avalanche and other networks:** Once you have configured your wallet, you will be ready to interact with the **Avalanche blockchain** and other networks compatible with **EVM**. Core automatically connects to the main Avalanche network (Avalanche C-Chain), but you can also add other networks manually.

### Security in Wallets

One of the most important aspects to consider when using wallets is **security**. Here are some key points to ensure that your cryptocurrencies are always protected:

* **Never share your private key or seed phrase**: The private key is the only way to access your funds. If someone gets your private key or seed phrase, they can steal all your cryptocurrencies without you having a chance to recover them.
* **Use strong passwords and two-factor authentication (2FA)**: If you use a software wallet (hot) or custodial, always enable additional security measures like 2FA to protect your account.
* **Regularly back up your seed phrase**: Save the seed phrase in a safe place, preferably offline, like a piece of paper or a cold storage device.
