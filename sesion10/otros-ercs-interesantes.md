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

# Other Interesting ERCs

As the Ethereum ecosystem has evolved, many other ERC standards have been created to expand the functionalities of smart contracts. Below, we present some of the most interesting ERCs that complement or extend the capabilities of ERC20, ERC721, and ERC1155.

### **ERC777 - Advanced Tokens with Hooks**

**ERC777** introduces the possibility of executing "hooks" in each token transfer, providing more flexibility and security. It is compatible with ERC20 but enhances its functionality by allowing contracts to react to transfers.

* **Features**:
  * Allows contracts to intercept and process transfers.
  * Improves efficiency in complex transactions.
* **Application**: Used in decentralized financial applications (DeFi) where automated actions are needed, such as fees or notifications.

### **ERC4626 - Standardized Vaults for Tokens**

**ERC4626** is a standard for "vaults" that store tokens, facilitating the development of DeFi applications where users can deposit tokens into a common pool.

* **Features**:
  * Provides a standard API for token deposits and withdrawals.
  * Facilitates interoperability between DeFi protocols that use vaults.
* **Application**: Used in staking and yield farming platforms, allowing users to deposit and earn returns in a standardized manner.

### **ERC998 - Composite or Hierarchical Ownership Tokens**

**ERC998** allows creating composite tokens where one token can "own" other tokens, which is ideal for complex digital assets.

* **Features**:
  * An NFT can own other NFTs or ERC20 tokens.
  * Enables hierarchical ownership structures.
* **Application**: Popular in games and virtual worlds, where characters or items can contain other objects or digital resources.

### **ERC725 - Decentralized Identity**

**ERC725** is a standard for digital identity on Ethereum, providing a system for identity profiles that users control.

* **Features**:
  * Support for secure storage of personal data.
  * Facilitates the creation of verifiable identities on the blockchain.
* **Application**: Useful for digital identity applications and decentralized KYC (Know Your Customer) verifications.

### **ERC948 - Subscriptions on the Blockchain**

**ERC948** defines a system for recurring payments and subscriptions on the blockchain, providing a structure for recurring payment services.

* **Features**:
  * Designed for automatic and recurring payments.
  * Ideal for decentralized subscription services.
* **Application**: Perfect for subscription services like content platforms, allowing automatic payments without intermediaries.

### **ERC1400 - Security Tokens**

**ERC1400** is a standard specifically created for security tokens, with advanced features for access control, compliance, and transparency, meeting legal regulations.

* **Features**:
  * Access controls and transfer restrictions.
  * Transparency and regulatory compliance.
  * Token hold and release events.
* **Application**: Used in security token offerings (STO) and financial applications where compliance with securities regulations is required.

### **ERC6551 - NFT-Associated Accounts**

**ERC6551** allows each NFT to have an associated contract account, expanding the possibilities of NFTs by enabling them to perform transactions and own other assets.

* **Features**:
  * Each NFT has an independent contract account.
  * Allows NFTs to own other assets.
* **Application**: Useful in games and virtual worlds where NFTs represent characters or items that can interact with other contracts or own their own assets.

### **ERC4973 - Bound Accounts**

**ERC4973** is a standard for creating "bound accounts" where an account is directly associated with a token and cannot be transferred or separated from it.

* **Features**:
  * Support for non-transferable tokens, designed for identity or membership.
  * Creates a binding between an account and a specific token.
* **Application**: Ideal for certificates, badges, and non-transferable personal assets, where a direct association between a user and the token is needed.

### **ERC1726 - Dividend Distribution Tokens**

**ERC1726** defines a standard for tokens that distribute dividends, allowing holders to automatically receive generated income, such as dividends or payments from tokenized loans. This standard facilitates the visualization and management of distributed dividends, helping holders receive their earnings efficiently.

* **Features**:
  * Defines a standard interface for querying cumulative and available dividends.
  * Compatible with ERC20 and other income-generating token standards.
* **Application**: Ideal for tokens representing rights to future cash flows, such as dividends or loan payments on DeFi platforms, ensuring transparent and wallet/exchange-compatible distribution.
