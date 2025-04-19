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

# Fallback and Receive

The **`fallback`** and **`receive`** functions in Solidity are super useful when your contract receives calls that don't match any of its functions or when someone sends Ether to your contract.

### `fallback`: the backup plan

The `fallback` function is like the contract's plan B. It's triggered when someone tries to interact with your contract by calling a function that doesn't exist. It's like if someone knocks on the wrong door and instead of waiting, the contract opens the door and says: "Sorry, that function isn't here, but what do you need?".

**Characteristics of `fallback`:**

* It cannot have arguments or return values.
* It can be declared as `payable` to accept Ether, or not, if it's only used to handle incorrect calls.
* It doesn't have a specific name, it's defined simply with the `fallback` keyword.

**Syntax:**

```solidity
fallback() external {
    // Logic to execute if a non-existent function is called
}
```

If you want it to also accept Ether, you declare it as `payable`:

```solidity
fallback() external payable {
    // Logic to execute if a non-existent function is called or Ether is sent
}
```

### `receive`: the payment doorman

The `receive` function is specifically triggered when the contract receives Ether, but no additional data is provided or any function is specified. It's like a doorman who only opens the door if someone wants to leave money.

**Characteristics of `receive`:**

* It's only triggered when Ether is sent without data (without `msg.data`).
* It cannot have arguments or return values.
* It must be declared as `payable` to accept Ether.

**Syntax:**

```solidity
receive() external payable {
    // Logic to execute when receiving Ether
}
```

### Practical example: Donation contract

Let's see how to use `fallback` and `receive` together in a donation contract:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Donations {
    // Event to record received donations
    event DonationReceived(address donor, uint amount);

    // Mapping to keep track of donations by user
    mapping(address => uint) public donations;

    // `receive` function that is triggered when receiving Ether without data
    receive() external payable {
        donations[msg.sender] += msg.value;
        emit DonationReceived(msg.sender, msg.value);
    }

    // `fallback` function to handle calls to non-existent functions
    fallback() external payable {
        donations[msg.sender] += msg.value;
        emit DonationReceived(msg.sender, msg.value);
    }

    // Function to query the total donated by a user
    function totalDonated(address user) public view returns (uint) {
        return donations[user];
    }
}
```

How does this contract work?

1. **receive()**: When someone sends Ether to the contract without specifying data, this function is triggered, the donation is recorded, and an event is emitted so everyone knows who donated how much.
2. **fallback()**: If someone tries to call a function that doesn't exist and, in addition, sends Ether, `fallback` is triggered. In this case, the donation is also recorded as in `receive`.
3. **totalDonated()**: Allows querying how much a specific user has donated. This type of function is useful for keeping records and giving transparency to the process.

### Differences between `fallback` and `receive`

* **`receive`** is only triggered when the contract receives Ether without data (empty `msg.data`).
* **`fallback`** is triggered when a non-existent function is called, with or without Ether, as long as `msg.data` is not empty (although it also works if there is no `receive` function defined).
