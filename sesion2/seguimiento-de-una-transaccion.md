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

# Tracking a Transaction

Now that we understand how we interact with the blockchain through cryptographic keys and wallets, it's time to explore **what happens when we make a transaction** and how we can track each step of the process in the **Avalanche** network.

This is where **block explorers** come into play. Think of these explorers as windows that allow us to see inside the blockchain. For example, if we use Bitcoin we have **Blockchain.info**, for Ethereum there's **Etherscan**, and in the case of **Avalanche** we have **SnowTrace**.

Imagine you want to send **AVAX**, the native cryptocurrency of Avalanche, to a friend. From the moment you decide to make this transaction until it's confirmed on the blockchain, several interesting steps occur that are worth knowing.

### Step 1: Initiating the transaction from your Wallet

Everything begins when you open your wallet, for example, **Core** or **MetaMask**, and decide to send a specific amount of AVAX to your friend's address. You enter the recipient's address, the amount to send, and adjust the transaction settings if necessary, such as gas fees.

When you press the **"Send"** button, your wallet creates a **transaction** that includes:

* **Your public address** (sender).
* **Your friend's public address** (recipient).
* **The amount** of AVAX you want to transfer.
* **Additional information**, such as transaction fees and a **nonce**, which is a number that ensures each transaction is unique.

### Step 2: Signing the transaction with your private key

Before the transaction can be sent to the network, it needs to be **digitally signed**. Your wallet uses your **private key** to generate a unique cryptographic signature. This signature ensures that the transaction was authorized by you and hasn't been altered along the way.

It's important to note that your private key is never sent to the network, only the resulting signature, which keeps your information secure.

### Step 3: Transmitting the transaction to the Avalanche network

Once signed, your wallet sends the transaction to the **Avalanche** network. This is where **nodes** come into action. Nodes are computers that maintain a copy of the blockchain and validate the transactions they receive.

### Step 4: Transaction validation by nodes

Avalanche nodes use the **consensus mechanism** of **Avalanche Consensus**, which is known for its high speed and efficiency. This process involves:

* **Random sampling**: Each node selects a small random subset of other nodes to query about the validity of the transaction.
* **Metastability**: Through multiple rounds of querying, nodes quickly reach an agreement on whether the transaction is valid or not.

During this process, nodes verify that:

* The transaction signature is valid and matches the sender's address.
* The sender has sufficient funds to cover the transaction amount and fees.
* There are no double-spending attempts, meaning the same funds aren't being used in another simultaneous transaction.

### Step 5: Including the transaction in a block

Once the transaction is validated, it's included in a **block** along with other transactions. Due to the efficiency of Avalanche's consensus mechanism, this process occurs in less than a second.

### Step 6: Transaction confirmation

After the block is added to the blockchain, the transaction is considered **confirmed**. In Avalanche, transactions typically reach finality almost instantly, which means you don't need to wait long periods for your transaction to become irreversible.

### Step 7: Verifying the transaction in SnowTrace

To make sure everything went well, you can verify your transaction in the **SnowTrace** block explorer. Follow these steps:

1. **Get the transaction hash**: Your wallet will provide you with the **hash** or unique identifier of the transaction once it's been sent. In this case, we'll follow a transaction I made sending 1 AVAX to another address, this was the generated hash:

```
0x2de74e0c605005295d8abef6ce2e7f37f2c39106183e8d3b07665dfb7d1bdab6
```

2. Access SnowTrace: In this case, we'll access the testnet, where tests are performed without having to spend real money.

{% embed url="https://testnet.snowtrace.io/" %}

3. **Enter the hash in the search bar**: Paste the transaction hash I gave you in step 1 into the search bar and press _Enter_.
4. **Review the transaction details**:

    * **Blockchain:** Should show **Fuji** (Avalanche test network)
    * **Transaction status**: Should appear as **Success**.
    * **Block**: Number of the block in which your transaction was included.
    * **Inclusion time (timestamp)**: You'll see the timestamp indicating when it was processed.
    * **Addresses**: The sender and recipient addresses.
    * **Amount and fees**: The amount sent (1.00 AVAX) and the fees paid (Fee).

    <figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

This transparency is one of the fundamental pillars of blockchain technology. We can all verify our transactions without the need for intermediaries or centralized entities. Additionally, we increase our trust in the system and in the operations we perform.

However, it's important to mention that although transactions are public, our identities remain anonymous. The blockchain shows addresses and amounts, but doesn't reveal personal information, thus maintaining our privacy.
