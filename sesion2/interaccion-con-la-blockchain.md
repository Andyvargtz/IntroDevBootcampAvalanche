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

# Interaction with the Blockchain

Another fundamental aspect to understand how we relate to the blockchain is **interaction through cryptographic keys**, specifically the **public and private keys** we mentioned earlier. These keys are essential for making transactions and ensuring security and authenticity in the network.

**Asymmetric cryptography** is the heart of this process. It's based on the generation of a key pair. The private key is like the key to your digital safe, while the public key is like your postal address where others can send you information or, in this case, cryptocurrencies.

### Bits and Bytes

Before going deeper, it's important to understand what **bits** and **bytes** are and their difference. A **bit** is the smallest unit of information in computing and can have a value of **0** or **1**. A **byte** is composed of **8 bits** and is a commonly used unit to represent larger amounts of data. For example, a character in ASCII text generally occupies 1 byte (8 bits).

When we talk about a **256-bit** private key, we're referring to a sequence of 256 binary digits (zeros and ones). This equals **32 bytes** (256 bits ÷ 8 bits per byte).

### Entropy in key generation

**Entropy** is a key concept in cryptography and refers to the degree of randomness or uncertainty in key generation. The more entropy a system has, the more unpredictable it will be, which increases security.

When generating a private key in blockchain, a sufficient amount of entropy is used to ensure that each generated key is unique. That's why it's crucial that the tools you use to generate keys are trustworthy and capable of producing enough entropy to avoid vulnerabilities.

### Key Generation in Bitcoin

In Bitcoin, keys are generated using cryptographic algorithms based on **elliptic curve cryptography** (ECC), specifically the **secp256k1** curve. This process involves generating a random 256-bit number (32 bytes), which becomes your private key. From this private key, the public key is calculated through mathematical operations on the elliptic curve.

The resulting public key is a longer sequence. In Bitcoin, addresses are derived from the public key by applying hash functions (SHA-256 and RIPEMD-160) and a special encoding called Base58Check, which produces a shorter and more manageable address.

For a practical experience, you can use online tools that allow generating these key pairs for educational purposes. For example, the website [**bitaddress.org**](https://www.bitaddress.org) is an open-source tool you can use to generate Bitcoin private and public keys without needing to install a wallet. However, it's important to remember that for security reasons, you should never use private keys generated online to manage real funds.

```
// Example of private key:
L4jzJwZvVgxfWWN2izdpJMS8VhBaEQohG3tNjPGFDVyQfoS8tXwA

// Example of Bitcoin Address:
1CKNwh13y792L3Lebntu3R1GUrGFqcDRRG
```

### Key Generation in Ethereum

In **Ethereum**, and in compatible networks like Avalanche, the process is similar but with some key differences. Ethereum also uses elliptic curve cryptography with the same **secp256k1** curve. The private key is a random 256-bit number (32 bytes, 64 hexadecimal characters). From this private key, the public key is generated, which is a sequence of **128 characters** hexadecimal (512 bits or 64 bytes), which includes the **X** and **Y** coordinates of the elliptic curve.

However, to make the process more efficient, **Ethereum compresses the public key**. Instead of storing both coordinates (**X** and **Y**), only the **X** coordinate is stored, along with an additional bit that allows calculating **Y**. This compression reduces the public key to **66 characters** hexadecimal (33 bytes), making key handling more efficient without compromising security.

To obtain the **Ethereum address**, the **Keccak-256** hash function is applied to the compressed public key and the last **40 characters** hexadecimal (20 bytes) are taken. By convention, the prefix '0x' is added at the beginning to indicate that it's a hexadecimal value. The Ethereum address therefore has **42 characters** (including '0x').

To generate your own keys in Ethereum in a practical and educational way, you can use tools like [**vanity-eth.tk**](https://vanity-eth.tk/). This page allows generating Ethereum private keys and addresses directly in your browser, without needing to download additional software. Again, remember that this practice should be only for educational purposes and not for managing real funds.

```
// Private key (64 characters):
1c39abf0e8e0f8eab0a0f5c7d9e1d3b2f4a5c6d7e8f9a0b1c2d3e4f5a6b7c8d9

// Public key (128 characters):
04a34b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5

// Ethereum address (42 characters):
0xA9962326BFaf46775B345f85aA9a649867EA5D56
```

### Seed Phrase

In addition to the private key, it's also common to generate a **seed phrase**. This is a sequence of words that acts as a backup for your private key. The seed phrase is usually composed of **12 or 24 words** chosen from a standardized list.

```
// Seed phrase (12 words):
poet bird river sky moon field mountain light shadow time flower wind
```

The seed phrase comes from a random number with a high level of entropy, and then, this number is converted into a series of words selected from the standardized list. It's crucial to keep this phrase in a safe place, as anyone who has access to it will be able to control your private key.

### Generate your Ethereum address securely

I'll guide you step by step so you can generate your key pair, seed phrase, and Ethereum address in a few steps. All through a library created by me exclusively for this course.

1. Download and install [Node.js](https://nodejs.org/en/).
2. Open the command terminal.
3. Run the following command to install the library:

```
npm install -g eth-key-generator
```

4. Once installed, you can run the tool from the command line:

```
eth-key-generator
```

5. You can choose between generating the address randomly or by providing entropy for greater security (you just need to enter a text string with any word or phrase).&#x20;
6. The tool will generate a new Ethereum address, showing each step of the process.

You can use this library as many times as you want, share it with more people, and you can even propose improvements, here's the link to the repository.

{% embed url="https://github.com/DavidZapataOh/ETH-KEY-GENERATOR" %}

{% hint style="info" %}
This tool is for educational purposes. Do not use the generated addresses to manage real funds without proper precautions.
{% endhint %}

### Here begins your journey

Once you have your keys, you can interact with the blockchain in several ways:

* **Send and receive cryptocurrencies**: You use your private key to sign transactions that transfer funds from your address to another. This signature ensures that the transaction was authorized by the legitimate owner.
* **Interact with smart contracts**: You can send transactions that execute functions in smart contracts. This allows you to interact in decentralized applications (dApps) and DeFi services.
* **Sign messages**: You can prove that you are the owner of an address by signing messages with your private key, without revealing the key itself. This is useful for authentications and verifications on different platforms.
