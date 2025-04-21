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

# What is an ERC

An **ERC** (Ethereum Request for Comments) is like an instruction manual for building different types of smart contracts on the Ethereum blockchain. Think of it as a set of rules or standards that all developers follow to ensure their contracts work consistently and can easily interact with each other. Each ERC describes how a smart contract should behave to fulfill certain functionalities, such as creating tokens, implementing NFTs, or managing permissions and roles.

They are the blueprints and guides that everyone must follow to ensure that, for example, a token created by one developer can be recognized and used by another developer's applications.

### How are ERCs created?

ERCs are proposed as improvements to the Ethereum protocol. Any developer can propose a new standard through a document known as an EIP (Ethereum Improvement Proposal). The developer community reviews, debates, and ultimately decides whether the proposal is accepted as an official ERC standard.

**Process for creating an ERC:**

1. **Idea proposal:** A developer drafts an EIP describing their proposal. This includes the technical specification, purpose, and how it will affect the blockchain.
2. **Discussion:** The Ethereum community reviews and comments on the EIP. Improvements are suggested and potential issues or alternatives are discussed.
3. **Review and acceptance:** If the EIP successfully passes the review process and the community agrees, it becomes an official ERC.

### Examples of most common ERCs

1. **ERC-20:** This is the most well-known standard and is used to create fungible tokens, such as cryptocurrencies. It defines functions like `transfer`, `balanceOf`, and `approve` so that tokens can be easily exchanged between different applications.
   * **Uses:** Tokens like DAI, USDT, Pepe.
2. **ERC-721:** The standard for non-fungible tokens (NFTs). Each ERC-721 token is unique and has specific properties, making it perfect for representing digital assets like art, collectibles, or virtual real estate.
   * **Uses:** CryptoKitties, Bored Ape Yacht Club, and other digital collectibles.
3. **ERC-1155:** This standard combines the best of both worlds. It allows the creation of both fungible and non-fungible tokens in the same contract, optimizing space and gas usage.
   * **Uses:** Games and collectibles like Gods Unchained and Enjin, where a single contract can manage weapons, abilities, characters, and coins.

### Why are ERCs important?

1. **Compatibility:** ERCs ensure that tokens and smart contracts behave predictably, allowing developers to build interoperable applications without having to reinvent the wheel.
2. **Security and trust:** By following a well-defined standard reviewed by the community, developers can avoid common errors and security flaws in their smart contracts.
3. **Innovation:** ERCs are a way to standardize new functionalities on the blockchain. They allow developers to quickly propose and adopt new features that benefit the entire ecosystem.
