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

# Visibility

**Visibility** defines who can see or interact with your contract's variables and functions. Think of visibility like privacy filters on your social networks - do you want your post to be seen by everyone, only your friends, or just yourself? It's the same here, but in code. Controlling visibility well is key to keeping your contract secure and organized, so let's review the available options and how to use them.

### Visibility for functions

1.  **`public`**: Everyone is welcome! `public` functions can be called from inside the contract, by other contracts, and also from outside, like from a user interface or directly from Core. They're like your public profile, visible to everyone.

    ```solidity
    function greet() public returns (string memory) {
        return "Hello, world!";
    }
    ```

    With this function, anyone can call it and get the greeting.
2.  **`private`**: Only for you. `private` functions can only be called from the same contract. Not even contracts that inherit from this one can access them. They're like your direct messages, no one else can see or interact with them.

    ```solidity
    function calculateSecret() private view returns (uint) {
        return 42;
    }
    ```
3.  **`internal`**: Only for the family. `internal` functions are like `private` ones, but with a bit more openness. They can be called from the same contract and also from contracts that inherit from it. Imagine a closed group where only family members have access.

    ```solidity
    function multiply(uint a, uint b) internal pure returns (uint) {
        return a * b;
    }
    ```
4.  **`external`**: Only calls from outside. `external` functions are like `public` ones, but with a twist - they can only be called from outside the contract. This makes them a bit more gas efficient. It's like having a special back door that only opens from the outside.

    ```solidity
    function getValue() external view returns (uint) {
        return value;
    }
    ```

### Visibility for variables

The visibility of state variables is also important. It controls how and who can access the data stored in your contract.

1.  **`public`**: Just like with functions, a `public` variable is visible to everyone. Solidity automatically creates a getter function so you can access its value from outside the contract.

    ```solidity
    uint public publicNumber = 42;
    ```

    With this variable, you can see its value directly from outside the contract, without needing an additional read function.
2.  **`private`**: Only for your eyes. A `private` variable cannot be read or modified from outside the contract. Even derived contracts cannot access it directly. It's like a safe to which only you have the combination.

    ```solidity
    uint private secretNumber = 123;
    ```
3.  **`internal`**: Similar to `private`, but accessible to derived contracts. Ideal for sharing data within a family of contracts. It's like a shared document that only the family has access to.

    ```solidity
    uint internal internalNumber = 100;
    ```
4. **Unspecified**: If you don't specify a variable's visibility, it will be `internal` by default. So, if you want something to be public or private, it's better to declare it explicitly to avoid misunderstandings.

### Practical example with everything combined

Let's see how all this would look in a contract with functions and variables of different visibility levels:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract VisibilityExample {
    // Public variable: accessible to everyone
    uint public publicCounter = 0;

    // Internal variable: only accessible to this contract and derived ones
    uint internal internalCounter = 10;

    // Private variable: no one outside this contract can access it
    uint private secretCounter = 100;

    // Public function: everyone can call it
    function incrementPublic() public {
        publicCounter += 1;
    }

    // Private function: can only be called within the contract
    function incrementSecret() private {
        secretCounter += 1;
    }

    // Internal function: accessible to derived contracts
    function incrementInternal() internal {
        internalCounter += 1;
    }

    // External function: only calls from outside
    function getSecretCounter() external view returns (uint) {
        return secretCounter;
    }
}
```
