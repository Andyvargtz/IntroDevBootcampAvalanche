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

# View and Pure Modifiers

In Solidity, the **`view`** and **`pure`** modifiers are like "do not touch" and "look only" labels in a museum. They tell you what kind of interactions you can have with functions and whether they can modify the contract's state or not. Let's see what each one is about and when you should use them.

### `view`: Look only, don't touch

When a function has the `view` modifier, it means that this function **can read data from the contract**, but cannot modify it. It's useful for making queries without changing the contract's state. Imagine it's like when you ask someone what their favorite color is, you're not changing their answer, you're just getting information.

```solidity
function getBalance() public view returns (uint256) {
    return balance;
}
```

Here, the `getBalance` function only returns the value of the `balance` variable without modifying anything. Advantage? You don't need to spend gas to use it when calling it from outside the contract!

### `pure`: Neither touch nor look

The `pure` modifier takes things a step further. It indicates that the function **cannot read or modify the contract's state**. It's only used for operations that don't depend on data stored in the contract. It's like solving a math problem on a separate sheet, you're not looking at anything from the contract, you're just using pure logic.

```solidity
function add(uint256 a, uint256 b) public pure returns (uint256) {
    return a + b;
}

```

The `add` function takes two numbers, adds them, and returns the result. It doesn't need to access any contract variables to do this.

### Practical Example

Let's see an example that combines both types of functions:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ViewPureExample {
    uint256 counter;

    // Function that increments the counter (modifies state)
    function increment() public {
        counter += 1;
    }

    // 'view' function that reads the contract's state
    function getCounter() public view returns (uint256) {
        return counter;
    }

    // 'pure' function that performs a calculation without reading or modifying state
    function calculateSquare(uint256 x) public pure returns (uint256) {
        return x * x;
    }
}
```

* `increment`: Modifies the contract's state by increasing the counter.
* `getCounter`: Only reads the counter's value, without changing anything.
* `calculateSquare`: Performs a mathematical calculation without touching any contract variables.
