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

# Contract

No more warnings! Now we can continue with contract declarations. When working with **Solidity**, **contracts** are the core of everything. Each smart contract we create is basically a set of functions and data that can be stored and executed on the blockchain.

Every time you create a contract, what you're doing is defining the rules and actions that can be taken when someone interacts with that contract on the blockchain.

Declaring a contract in Solidity is quite simple. We use the `contract` keyword followed by the name you want to give to your contract, for example:

```solidity
contract MiPrimerContrato {
    // Here goes all the contract code
}
```

This is the basic structure for creating any contract in Solidity. Inside this block is where you'll define all the functions, variables, and events that make up your smart contract.

As you can see, PascalCase convention is used when declaring the contract name, meaning the first letter of each word is capitalized. Example: _ExampleOfPascalCase_.

Contracts in Solidity are similar to classes in object-oriented languages. Each contract can contain declarations of State Variables, Functions, Modifiers, Events, Errors, Struct Types, and Enum Types. Additionally, contracts can inherit from other contracts.

<figure><img src="../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>
