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

# Constants

**Constants** in Solidity are like those rules that never change, like "pineapple doesn't go on pizza" (although we know some people don't respect that constant). They are values that, once defined, cannot be modified, making them perfect for data that should never change, such as important addresses, maximum limits, or fixed contract configurations.

Defining constants in your contract helps you save gas, as their value is stored directly in the contract's bytecode and doesn't occupy space on the blockchain.

```solidity
uint256 public constant MAX_LIMIT = 1000;
address public constant TREASURY_ADDRESS = 0x1234567890123456789012345678901234567890;
```

Here, `MAX_LIMIT` and `TREASURY_ADDRESS` are constants that can never be changed. This is great for values that should not be modified under any circumstances.
