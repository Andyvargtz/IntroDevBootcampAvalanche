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

# Sending Ether from a Contract

Sending **Ether** from a contract in Solidity might seem complicated at first, but with the right methods, it's quite simple. Whether you want to make automatic payments, distribute rewards, or simply send funds to another address, it's important to understand how to do it safely and efficiently. Let's explore how to send Ether from a contract and what things you need to keep in mind to avoid problems.

### How do you send Ether from a contract?

In Solidity, there are three main ways to send Ether:

1. **Transfer**: It's the simplest and most direct way. It sends 2300 gas, enough to record an event and change the balance, but not to execute complex functions.
2. **Send**: Similar to `transfer`, but instead of throwing an error if the transaction fails, it returns `true` or `false`. It sends 2300 gas.
3. **Call**: It's the most versatile and secure. It allows you to send Ether and execute functions, plus control the gas sent.

#### Method 1: `transfer`

`transfer` is like the most direct and secure bank transfer, but also the most limited. If the send fails, it throws an error and reverts the transaction.

```solidity
function sendEtherTransfer(address payable destination) public payable {
    destination.transfer(msg.value);
}
```

* **Advantages**: Simple and secure.
* **Disadvantages**: If the recipient needs more than 2300 gas to complete their logic, the transaction will fail.

#### Method 2: `send`

`send` works the same as `transfer`, but instead of throwing an error, it simply returns `false` if the transaction fails. This is useful if you want to handle errors manually, but you must make sure to always verify the return value.

```solidity
function sendEtherSend(address payable destination) public payable {
    bool success = destination.send(msg.value);
    require(success, "Ether send failed");
}
```

* **Advantages**: Allows manual error handling.
* **Disadvantages**: Like `transfer`, it only sends 2300 gas, and if you don't check the return value, you might not realize the transaction failed.

#### Method 3: `call`

`call` is like the Swiss Army knife of Solidity. Not only can you send Ether, but you can also execute functions in the destination contract, plus control how much gas is sent. This is the recommended way for most cases, as it gives you more control and flexibility.

```solidity
function sendEtherCall(address payable destination) public payable {
    (bool success, ) = destination.call{value: msg.value}("");
    require(success, "Ether send failed with call");
}
```

* **Advantages**: Total control over gas and can execute functions in the destination.
* **Disadvantages**: You must be very careful with its use, because if misconfigured it can allow attacks like **reentrancy**.

### Practical Example: Profit Distribution

Let's look at an example where we use `call` to distribute Ether among multiple recipients:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Distribution {
    address payable[] public beneficiaries;
    
    // Add a beneficiary
    function addBeneficiary(address payable _newBeneficiary) public {
        beneficiaries.push(_newBeneficiary);
    }
    
    // Function to distribute Ether equally among all beneficiaries
    function distributeProfit() public payable {
        uint256 amountPerPerson = msg.value / beneficiaries.length;
        for (uint256 i = 0; i < beneficiaries.length; i++) {
            (bool success, ) = beneficiaries[i].call{value: amountPerPerson}("");
            require(success, "Ether send failed");
        }
    }
}
```

In this contract, `distributeProfit` distributes the Ether sent to the function among all stored beneficiaries. It uses `call` to send the Ether, ensuring that each transaction completes correctly.

### Things to keep in mind

1. **Reentrancy Attacks**: When using `call` to send Ether, make sure your logic is well structured to prevent reentrancy attacks. An attacker could try to call your contract again before the first call finishes, which could cause serious problems. Always use the **Checks-Effects-Interactions** pattern: first verify conditions, then update state, and finally perform external interaction (sending Ether).
2. **Gas Usage**: `transfer` and `send` only send 2300 gas, which is not enough for complex functions in the receiving contract. If you need more gas, use `call` and specify the necessary amount.
3. **`payable` Addresses**: You can only send Ether to addresses marked as `payable`. Make sure to use `address payable` for recipients.
