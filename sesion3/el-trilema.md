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

# The Trilemma

The **Blockchain Trilemma** is a term that was popularized by **Vitalik Buterin.** It basically states that there are three essential properties that a blockchain should have, but it is extremely difficult (if not impossible) to achieve all three at the same time. These are:

* **Security**
* **Decentralization**
* **Scalability**

The dilemma arises because, in practice, when trying to optimize one of these properties, you generally sacrifice one or both of the others. Let's look more deeply at each of these:

### Security

It is probably the most important aspect in any blockchain. At the end of the day, people want to know that their digital assets are secure and that the network won't be vulnerable to attacks or manipulations. For a blockchain to be truly secure, it must be resistant to things like 51% attacks, where an attacker could potentially take control of the network if they gain enough computational power or participation.

In blockchains like Bitcoin and Ethereum, security is guaranteed by mechanisms such as **Proof of Work** or **Proof of Stake**, where validators have to spend resources (either energy or capital in the form of ETH) to secure the network.

### Decentralization

Means that no single entity or group has control over the network. In a truly decentralized blockchain, anyone can join as a node or validator, and there is no central authority dictating the rules. This is what gives blockchain its power to be censorship-resistant and to operate without intermediaries.

The problem is that achieving a high level of decentralization usually makes it harder to scale the network. The more nodes and validators you have, the more time and resources may be needed to coordinate all those participants and reach consensus.

### Scalability

Refers to a blockchain's ability to handle a large number of transactions in a short period of time. Ethereum 1.0, for example, had problems with scalability, as it could only process between 15 and 30 transactions per second. This might sound good until you realize that centralized networks like Visa can process thousands of transactions per second.

When a blockchain is not scalable, it becomes slow and transaction fees skyrocket. This was one of the main problems that Ethereum faced before beginning its transition to Ethereum 2.0.

### Why is it so complicated?

This is where the real dilemma comes in. Improving one of these three characteristics almost always implies compromising the other two. For example:

* If you try to increase **scalability** you often sacrifice **decentralization**. By allowing only a few nodes or validators to handle most transactions, you lose part of that decentralized nature that makes blockchain censorship-resistant.
* If you focus on pure **decentralization**, like Bitcoin, then it's hard to scale the network, as each node needs to process and validate each transaction individually, which can slow everything down.
* And if you prioritize **security**, as happens in many blockchains, the effort and resources needed to secure the network can make it difficult to scale.

### The Trilemma in Ethereum

Ethereum in its early versions had to face this trilemma head-on. The network wanted to be **secure** and **decentralized**, but that led to **scalability** problems, as we saw with high gas fees and network congestion.

With Ethereum 2.0 and the introduction of technologies like **Proof of Stake** and **sharding**, the network seeks a solution that improves **scalability** without sacrificing too much in terms of **security** and **decentralization**. Sharding allows the workload to be divided among multiple fragments, increasing the number of transactions that can be processed without having to compromise the network's decentralization.

The Trilemma remains a challenge without a definitive solution, but many developers and projects are working on how to address this problem. From Ethereum's side, there are Layer 2 solutions, which we will see later.
