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

# Consensus Mechanisms

One of the fundamental pillars that made Bitcoin's operation possible was the consensus mechanism called **Proof of Work**. This system allows all **nodes** in the network to agree on the state of the blockchain without the need for a central authority.

But, what is a node? A node is any device, such as a computer, that connects to the blockchain and maintains an updated copy of the entire blockchain, participating in the validation and propagation of transactions.

### Proof of Work

Miners, who are special nodes, compete to solve complex mathematical problems, and the first one to find the solution can add the next block of transactions to the chain, receiving a reward for their effort.

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption><p><a href="https://whiteboardcrypto.com/what-is-proof-of-work/">https://whiteboardcrypto.com/what-is-proof-of-work/</a></p></figcaption></figure>

However, with the growth of the network and the increase in calculation difficulty, **Proof of Work** has shown certain limitations. High energy consumption and slow transaction confirmation have become major obstacles along the way. It was then that new proposals emerged to improve the efficiency and scalability of blockchains.

### Proof of Stake

This is where **Proof of Stake** comes into play. Instead of relying on computational power, this mechanism selects **validators** based on the amount of cryptocurrency they own and are willing to "stake" as collateral.&#x20;

But, who are these validators? Validators in **Proof of Stake** are network participants who lock up a portion of their coins as a commitment that they will act honestly. If they validate fraudulent transactions, they can lose their staked funds. This drastically reduces energy consumption and speeds up the transaction validation process.&#x20;

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption><p><a href="https://tangem.com/en/blog/post/proof-of-stake-pos-the-main-concept-and-principles/">https://tangem.com/en/blog/post/proof-of-stake-pos-the-main-concept-and-principles/</a></p></figcaption></figure>

**Ethereum**, recognizing these advantages, made its transition from Proof of Work to Proof of Stake with the goal of improving its performance and scalability. But innovation in consensus mechanisms doesn't stop there. In 2020, **Avalanche** emerged, a blockchain ecosystem that introduces a new and revolutionary consensus protocol known as **Avalanche Consensus**. This mechanism combines the best of previous systems and adds significant improvements.

### Avalanche Consensus

**Avalanche Consensus** uses an approach based on "metastability" and repeated random sampling, meaning that instead of all nodes validating all transactions, each node queries a small random subset of other nodes. Through multiple rounds of querying, the network **quickly reaches an agreement** without sacrificing security or decentralization.

This method allows **Avalanche** to achieve transaction finality times of **less than one second** and the capacity to process **thousands of transactions per second**. Additionally, it is highly resistant to attacks and doesn't require high energy consumption, making it one of the best solutions currently available.

<figure><img src="../.gitbook/assets/get-started-avax-consensus.gif" alt=""><figcaption></figcaption></figure>
