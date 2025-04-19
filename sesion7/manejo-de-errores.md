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

# Error Handling

**Error handling** in Solidity is key to making your contracts work safely and predictably. Imagine you're playing a video game, if your character tries to jump over a cliff and the game doesn't have a way to handle that error, you simply fall into the void and the game breaks. Well, something similar happens in Solidity. Without proper error handling, the contract can behave unexpectedly and users can lose money or resources.

### Why is error handling important?

When you execute a contract, many things can go wrong: you try to transfer more Ether than you have, you call a function with incorrect parameters, or there's a bug in the logic. If you don't control these errors, the contract can behave unpredictably and cause problems. Using the right tools for error handling ensures that if something goes wrong, the contract stops safely and returns unused gas.

### Tools for error handling in Solidity

1.  **`require`**: Verifies that a condition is met before continuing with execution. If the condition fails, it reverts the transaction, returns unused gas, and displays an error message. Perfect for validating user inputs or function results.

    ```solidity
    function withdrawFunds(uint amount) public {
        require(amount <= balance[msg.sender], "You don't have enough funds");
        balance[msg.sender] -= amount;
    }
    ```

    Here, `require` ensures that the user doesn't try to withdraw more than they have. If the condition isn't met, the contract stops and displays the error message "You don't have enough funds".
2.  **`revert`**: Similar to `require`, but used to revert transactions in more complex situations, where it's not possible to evaluate the condition directly in the same line. It can also be used with a custom message.

    ```solidity
    function transfer(address recipient, uint amount) public {
        if (amount > balance[msg.sender]) {
            revert("Insufficient funds");
        }
        balance[msg.sender] -= amount;
        balance[recipient] += amount;
    }
    ```

    Here, `revert` stops execution if the user tries to transfer more funds than they have, showing the message "Insufficient funds".
3.  **`assert`**: Used to verify internal conditions that should always be true. If `assert` fails, it means something is very wrong with the contract and execution stops immediately without returning the gas used.

    ```solidity
    function testImmutable(uint x) public pure returns (uint) {
        assert(x != 0); // x should never be 0
        return 100 / x;
    }
    ```

    Here, `assert` ensures that `x` is not 0. If it is, something serious is happening, and the contract stops completely.

### **Custom errors in `require` and `revert`**

To handle specific errors and send detailed messages, you can define custom errors. These errors allow you to provide more information about why an operation failed, and they are more gas efficient.

```solidity
error InsufficientFunds(uint requested, uint available);

function withdraw(uint amount) public {
    if (amount > balance[msg.sender]) {
        revert InsufficientFunds({
            requested: amount,
            available: balance[msg.sender]
        });
    }
    balance[msg.sender] -= amount;
}
```

In this example, if the user tries to withdraw more than they have, the `InsufficientFunds` error is triggered, indicating how much was requested and how much was available. This provides an extra level of detail that can be very useful for users.

### What's the difference between `require`, `revert`, and `assert`?

* **`require`**: Used to validate conditions that depend on external inputs, such as function parameters or the current state of the contract. If it fails, the transaction is reverted and unused gas is returned.
* **`revert`**: Used to handle more complex conditions where you need to manually control how and when the transaction is reverted. It also reverts the transaction and returns unused gas.
* **`assert`**: It's more drastic. It verifies internal conditions that should always be met. If it fails, it's because there's a critical error in the contract's logic and it doesn't return the gas used.

### Practical example: Error handling in a bank contract

Let's imagine a contract that allows users to deposit and withdraw funds. If a user tries to withdraw more than they have, we want to stop the operation and show a specific message.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Bank {
    mapping(address => uint) public balances;

    // Define a custom error
    error InsufficientFunds(uint requested, uint available);

    // Function to deposit funds
    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    // Function to withdraw funds
    function withdraw(uint amount) public {
        if (amount > balances[msg.sender]) {
            revert InsufficientFunds(amount, balances[msg.sender]);
        }
        balances[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
    }

    // Function to check balance
    function getBalance() public view returns (uint) {
        return balances[msg.sender];
    }
}
```

In this contract, if you try to withdraw more funds than you have, the `InsufficientFunds` error is triggered and shows exactly how much was attempted to be withdrawn and how much was available.
