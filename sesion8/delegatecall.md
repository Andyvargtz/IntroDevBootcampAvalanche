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

# DelegateCall

The `delegatecall` method in Solidity is like allowing someone to use your identity to perform actions on your behalf. Basically, it executes another contract's code but using your own contract's context, which means it can change your contract's state and variables as if they were its own. It's a powerful tool, but also risky if not used correctly, as it gives control over your contract to external code.

### What is `delegatecall`?

`delegatecall` is a low-level function that allows a contract to execute another contract's code as if it were its own. This means that the state variables, ether balances, and other properties of the contract making the `delegatecall` are affected, not those of the contract containing the code.

**Basic syntax:**

```solidity
(bool success, bytes memory data) = address.delegatecall(abi.encodeWithSignature("functionName(parameters)"));
```

* `success` is a boolean indicating if the call was successful.
* `data` contains the data returned by the called function.
* `address` is the address of the contract you're calling.
* `abi.encodeWithSignature` encodes the function signature and its parameters.

### How does `delegatecall` work?

Let's imagine you have two contracts, a main contract (`Main`) and a logic contract (`Logic`). The `Main` contract delegates the execution of certain functions to the `Logic` contract. This is useful when you want to update your contract's logic without changing its state, like changing your contract's "brain" while keeping the same body.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Logic contract containing the functions we want to execute
contract Logic {
    uint public number;

    // Function to set the number, but using the storage of the calling contract
    function setNumber(uint _number) public {
        number = _number;
    }
}

// Main contract that uses `delegatecall` to execute functions from the logic contract
contract Main {
    uint public number;

    // Address of the logic contract
    address public logicAddress;

    // Constructor to initialize the logic contract address
    constructor(address _logicAddress) {
        logicAddress = _logicAddress;
    }

    // Function that uses `delegatecall` to call `setNumber` in the logic contract
    function executeDelegatecall(uint _number) public {
        (bool success, ) = logicAddress.delegatecall(
            abi.encodeWithSignature("setNumber(uint256)", _number)
        );
        require(success, "Delegatecall failed");
    }
}
```

1. **`Logic` Contract**: Contains a `setNumber` function that modifies the value of `number`.
2. **`Main` Contract**: Uses `delegatecall` to call the `setNumber` function in the `Logic` contract.
3. **Execution in the `Main` contract's context**: Although `setNumber` is a function of the `Logic` contract, `delegatecall` makes the `number` variable that gets modified be the one in the `Main` contract, not the one in the `Logic` contract.

### Why use `delegatecall`?

`delegatecall` is extremely useful when you want to update your contract's logic without changing its address or state. This is very common in design patterns like **proxy patterns**, where a proxy contract delegates all calls to another contract that contains the logic. If you need to change the logic, you simply point the proxy to a new logic contract, and that's it.

### Advantages and disadvantages of `delegatecall`

**Advantages:**

1. **Logic updates**: You can change the contract's logic without changing its address or state.
2. **Code reuse**: Use the same logic contract for multiple contracts, reducing code duplication.
3. **Simplified maintenance**: If you need to fix or improve the logic, you only need to update the logic contract, not the main one.

**Disadvantages:**

1. **Security risk**: If the logic contract has security flaws, these are transferred to the main contract. Also, if someone can change the logic contract's address in the main contract, they can point to a malicious contract.
2. **Storage confusion**: `delegatecall` uses the main contract's storage, which can lead to errors if you're not careful with variable organization.

### Security considerations

When using `delegatecall`, make sure that the contract you're calling is trustworthy and its code is well-audited. Changing the logic contract's address in the main contract must be very well protected, as otherwise someone could redirect all calls to a malicious contract.
