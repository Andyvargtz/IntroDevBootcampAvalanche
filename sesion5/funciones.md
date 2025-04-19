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

# Functions

**Functions** in Solidity are the backbone of any smart contract. They are reusable blocks of code that allow interaction with the contract, modify its state, execute logic, and return results. Let's break down everything you need to know about functions, from their basic structure to the different visibility options and modifiers you can use to control their behavior.

### What is a function in Solidity?

A function in Solidity is a set of instructions that perform a specific task. Each time a function is invoked, its code is executed and, depending on its design, it can read or modify the contract's state, interact with other contracts, or even return values.

```solidity
function greet() public pure returns (string memory) {
    return "Hello, Avalanche!";
}
```

In this example, `greet` is a simple function that returns a greeting. Let's break down the main elements:

1. **`function`**: The keyword to define a function.
2. **`greet`**: The name of the function.
3. **`public`**: Specifies the visibility of the function.
4. **`pure`**: Indicates that the function does not access or modify the contract's state.
5. **`returns (string memory)`**: Specifies that the function returns data, in this case a text string.

### Parameters

Functions in Solidity can receive **parameters** as input to execute specific logic. Parameters are variables that are passed to the function when it is called, allowing its behavior to be customized based on the provided values. Parameters are defined within the function's parentheses and can be of any data type.

```solidity
function setBalance(uint256 newBalance, address user) public {
    balances[user] = newBalance;
}
```

In this case, the `setBalance` function receives two parameters: `newBalance` (an integer) and `user` (an address). This allows setting the balance for any specific address.

### Types of Functions in Solidity

#### **1. State Functions**

These functions can modify the contract's state. That is, they can change the value of state variables.

```solidity
function setBalance(uint256 _balance) public {
    balance = _balance;
}
```

* `setBalance` is a function that modifies the state variable `balance`. This type of function incurs gas costs because it performs writes to the blockchain.

#### **2. Read-Only Functions**

These functions only read the contract's state and do not modify it. They are declared with the `view` modifier.

```solidity
function getBalance() public view returns (uint256) {
    return balance;
}
```

* `getBalance` returns the value of `balance` without modifying it. `view` functions do not incur gas costs when called externally (for example, from an interface).

### Function Examples

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Functions {
    uint8 age;

    // Function to set age (modifies state)
    function setAge(uint8 _age) public {
        age = _age;
    }

    // Function to get age (read-only)
    function getAge() public view returns (uint8) {
        return age;
    }

    // Pure function that adds two numbers
    function add(uint a, uint b) public pure returns (uint256) {
        return a + b;
    }

    // Function that calculates age in days (internal)
    function ageInDays() public view returns (uint16) {
        return age * 365;
    }
}
```

