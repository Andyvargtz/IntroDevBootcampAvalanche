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

# Anatomy of a Block

Now that we know how a transaction is made and how to track it on the blockchain, it's time to understand **what a block is** and what information it contains. After all, the blockchain is called that because it's made up of a chain of blocks. But what's inside those blocks?

A block contains several important parts:

1. **Block Header:**
   * **Previous Block Hash:** It's like a seal that connects each block with the previous one, forming an unbreakable chain. This ensures that previous blocks cannot be altered without changing all the ones that come after. However, in the case of the **Genesis Block**, which is the first block in the chain, this field is filled with zeros, since there is no previous block. This indicates that it is the starting point of the blockchain.
   * **Timestamp:** Indicates the date and time when the block was created. This way we know when everything happened.
   * **Nonce:** It's a number that miners have to find in order to add the block to the chain. In **Proof of Work**, miners compete to discover this number by solving mathematical problems.
   * **Merkle Root:** It's like a summary of all transactions in the block. It allows quick verification if a transaction is included without having to check them one by one.
2. **Block Body:**
   * **Transactions:** This is where all the transactions included in the block are recorded. Each one has details such as who sends, who receives, and how much is transferred.

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Essentially, a block would be like a box that contains many transactions and has important labels that connect it to the previous block and summarize its content.

With all blocks connected, if someone tried to change a transaction in a previous block, they would have to modify all subsequent blocks, which is practically impossible in a large network.

### Genesis Block

Speaking of blocks, we can't forget the famous **Genesis Block**. This is the first block of a blockchain, the starting point of everything. In Bitcoin's case, the Genesis Block was created by Satoshi Nakamoto on January 3, 2009. This block is special because it doesn't reference any previous block (because there simply wasn't one). Additionally, Satoshi included a hidden message in it: _"The Times 03/Jan/2009 Chancellor on brink of second bailout for banks"_, which was the headline of a British newspaper that day. Many see this as a criticism of the traditional financial system and a statement of intent about why Bitcoin was born.

The Genesis Block is fundamental because it establishes the initial rules and structure of the blockchain. Without it, there would be no chain to follow. Each block added afterward is based on the previous one, creating that blockchain we know.

Now when you hear about miners solving mathematical problems or blocks being added to the chain, you'll know exactly what it means and why it's so important. The blockchain is more than just a list of transactions, it's a carefully designed system to be secure, transparent, and resistant to manipulation.
