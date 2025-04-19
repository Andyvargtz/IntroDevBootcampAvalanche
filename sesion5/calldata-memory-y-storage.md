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

# Calldata, Memory and Storage

In Solidity, understanding how **calldata, memory, and storage** work is key to writing efficient contracts and avoiding errors. These three terms define where and how data is stored in the contract and have a direct impact on gas costs and contract functionality.

Let's break them down and see how to use each one effectively, with special attention to strings.

### Calldata, Memory and Storage

**1. Calldata: Temporary and Read-Only Data**

* You can view the data, but you cannot change it. It is used for input data of external functions and is **immutable** (you cannot modify the data that arrives here).
* **When to use it?**\
  Use it when you want to pass data to a function and don't need to change it. It's more gas efficient than `memory` because it avoids unnecessary data copying.
*   **Example:**

    ```solidity
    function processData(uint256[] calldata numbers) external pure returns (uint256) {
        return numbers[0] * 2; // We are only reading data, not changing it.
    }
    ```

    Here, `numbers` is an array of integers.

**2. Memory: Temporary Memory for Changing Data**

* It's useful while you need it, but nothing remains saved when you leave. This is where temporary data is stored within a function.
* **When to use it?**\
  It's used for data that you need to modify within the function or to handle intermediate data. Strings and arrays that are manipulated in functions must be in `memory` to work with them without restrictions.
*   **Example 1:**

    ```solidity
    function temporaryGreeting() public pure returns (string memory) {
        string memory message = "Hello, Avalanche!";
        return message; // The value of 'message' is only saved while the function executes.
    }
    ```

    When the function execution ends, `message` disappears, and no one remembers it existed.
*   **Example 2:**

    ```solidity
    function changeMessage(string memory message) public pure returns (string memory) {
        message = "Hello, Avalanche!";
        return message; // We can modify 'message' because it's in memory.
    }
    ```

    Here you can do whatever you want with `message`, change it, combine it, etc., because it's in `memory` and not in `calldata`.

**3. Storage: Permanent Storage on the Blockchain**

* `storage` is the contract's vault, where everything you want to last forever (or until someone changes it) is stored. This is where the contract's state variables are stored, such as balances or user data.
* **When to use it?**\
  It's used for data that must be persistent, such as user balances, contract owner, or any information you need to maintain even after the function ends.
*   **Example:**

    ```solidity
    uint256 public totalTokens; // This is in storage

    function setTokens(uint256 amount) public {
        totalTokens = amount; // We change the value in storage, and this has a gas cost.
    }
    ```

    Here, `totalTokens` is stored in storage, and any change you make will be permanent (well, at least until another transaction modifies it).



Using `calldata`, `memory`, and `storage` correctly not only optimizes gas usage but also prevents errors and unexpected behaviors. For example, if you pass a string as a parameter without specifying its location, Solidity won't know how to handle it and will throw a compilation error. That's why you should always declare strings and dynamic arrays as `calldata` or `memory` when passing them as parameters to a function.

**Common error example:**

```solidity
function changeMessage(string message) public { 
    // Error: It's not specified whether 'message' is in memory or calldata.
}
```

**Corrected version:**

```solidity
function changeMessage(string memory message) public { 
    // Now it's correct, because 'message' is in memory.
}
```
