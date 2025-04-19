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

# Mapping

**Mappings** are like dictionaries that allow you to store key-value pairs in a super efficient way. Imagine a large drawer with many labels (keys) and each label has a compartment where you store specific data (value). This is basically what mappings do - they allow you to search and store data in a quick and easy way.

### What is a mapping?

A `mapping` in Solidity is a data structure that associates keys with values, like a contact list where the key is the name and the value is the phone number. The syntax is:

```solidity
mapping(keyType => valueType) public mappingName;
```

For example:

```solidity
mapping(address => uint256) public balances;
```

In this case, the `mapping` `balances` associates addresses (`address`) with integers (`uint256`). This way each address has an associated balance that can be easily updated or queried.

### How do mappings work?

The interesting thing about mappings is that **every key always exists**, but if a value has never been assigned, it will return the default value of the corresponding data type (for example, `0` for integers, `false` for booleans, etc.). So if you query a `mapping` with a key you've never used before, it won't give you an error, but rather it will say something like "well, there's no data here yet, but if you want I can start storing what you tell me".

### Basic example:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Invitations {
    // We create a mapping for inviting users to a party
    mapping(address => bool) guests;

    // Function to invite a user
    function invite(address user) public {
        guests[user] = true;
    }

    // Function to check if a specific address has an invitation
    function checkGuest(address user) public view returns (bool) {
        return guests[user];
    }
}
</code></pre>

In this example, every time someone calls the `invite` function and passes an address as a parameter, their value in the `guests` mapping changes to `true`. You can check if any address is invited or not using `checkGuest`.

### Things you should know about mappings:

1. **You cannot iterate over a mapping**: Unlike an array, you cannot loop through all elements of a mapping. This means there's no easy way to "list" all stored keys. If you need to do that, you'll have to maintain a separate array with the keys or use some additional structure.
2. **Default values**: If you try to access a value that doesn't exist, the mapping will return the default value of the value's data type. This can be useful, but it can also lead to confusion if not handled correctly.
3. **Nested mappings**: You can have mappings inside mappings. For example, a mapping that associates addresses with another mapping of integers, like a super drawer with sub-drawers inside.
