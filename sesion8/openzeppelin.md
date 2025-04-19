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

# Openzeppelin

**OpenZeppelin** is a library that offers pre-designed and audited smart contracts that save you time and protect you from making common mistakes. If you're developing in Solidity and want to avoid reinventing the wheel (and also ensure your code is as secure as possible), OpenZeppelin is an essential tool.

### What is OpenZeppelin?

OpenZeppelin is a collection of modular and reusable smart contracts, designed to help you build decentralized applications quickly and securely. OpenZeppelin contracts have been extensively audited and tested, so using them significantly reduces the risk of introducing errors or vulnerabilities in your code.

**Main advantages:**

1. **Security:** OpenZeppelin contracts are developed and audited by security experts, minimizing the chances of vulnerabilities.
2. **Standardization:** Easily implement standards like ERC20, ERC721 (NFTs), and ERC1155, ensuring your contract complies with community specifications.
3. **Modularity:** You can customize and extend OpenZeppelin contracts to adapt them to your project's specific needs.

### What can you do with OpenZeppelin?

OpenZeppelin offers pre-designed contracts for a variety of use cases:

1. **ERC20 and ERC721 (NFTs) Tokens:** Easily implement your own fungible token (like a utility token) or non-fungible token (like a digital collectible).
2. **Roles and Permissions:** Control who can execute certain functions in your contract through role and permission contracts.
3. **Governance:** Build voting systems and proposal management for decentralized projects.
4. **Pausability and Security:** Implement functions to pause certain critical operations in your contract in case of emergency.

### Creating an ERC20 Token with OpenZeppelin

Let's create a simple ERC20 token using OpenZeppelin. Instead of writing the entire contract from scratch, we'll leverage OpenZeppelin's implementation to ensure the contract follows standards and is secure.

```solidity
// Import the ERC20 contract from OpenZeppelin
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    // Constructor to initialize the contract with name and symbol
    constructor() ERC20("My Token", "MTK") {
        // Assign all tokens to the contract creator
        _mint(msg.sender, 1000000 * (10 ** uint256(decimals())));
    }
}
```

What does this contract do?

1. **Importing the ERC20 contract:** We use OpenZeppelin's standard implementation to ensure the contract follows all ERC20 standard specifications.
2. **Contract initialization:** In the constructor, we initialize the name (`My Token`) and symbol (`MTK`).
3. **Initial minting:** We create 1 million tokens and assign them to the contract creator.

### Other notable OpenZeppelin features

1. **Ownable:** This contract is ideal for controlling access to specific functions, defining a contract owner who can transfer ownership to another user.
2. **Pausable:** Allows you to pause and resume certain critical contract functions. Very useful in emergency situations.
3. **SafeMath:** Prevents common problems like overflows and underflows in arithmetic operations. Although this is no longer necessary in more recent versions of Solidity, it's still good practice for older contracts.
