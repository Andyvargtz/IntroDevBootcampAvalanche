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

# Types of Variables

**Types of variables** are fundamental to define how information is stored and manipulated on the blockchain. Knowing how they work and the particularities of each variable type will allow you to write more efficient and secure contracts. Let's explore the different types of variables and their main characteristics.

### 1. **State Variables**

**State variables** are stored directly on the blockchain and maintain their value between function calls and transactions. They are persistent, and any change in their value implies a permanent modification on the blockchain.

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StorageTypes {

<strong>uint256 public totalSupply; // Permanently stored on the blockchain
</strong>address public owner; // Stores the address of the contract owner

// rest of the contract...
}
</code></pre>

### 2. **Local Variables**

**Local variables** only exist during the execution of a function. They are stored in memory and do not persist after the function has ended. They do not occupy space on the blockchain and are therefore cheaper to use.

```solidity
function calculateSum(uint256 a, uint256 b) public pure returns (uint256) {
    uint256 sum = a + b; // Local variable
    return sum;
}
```

#### 3. **Global Variables**

Solidity offers several **global variables** that provide information about the contract environment, such as the address of the transaction sender or the amount of gas available. Below, I show you a table with all the most important global variables and their description:

| **Global Variable**      | **Description**                                                                            | **Data Type** |
| ------------------------ | ------------------------------------------------------------------------------------------ | ---------------- |
| `msg.sender`             | Address of the account that invoked the function.                                              | `address`        |
| `msg.value`              | Amount of Ether (in wei) sent with the transaction.                               | `uint`           |
| `msg.data`               | Complete data sent with the function call.                                | `bytes`          |
| `msg.sig`                | First word (4 bytes) of `msg.data`, which identifies the function being called.   | `bytes4`         |
| `tx.origin`              | Address of the account that initiated the transaction (not just the current call).              | `address`        |
| `block.timestamp`        | Current block timestamp in seconds since the epoch.                                    | `uint`           |
| `block.number`           | Current block number.                                                                  | `uint`           |
| `block.coinbase`         | Address of the miner who validated the current block.                                          | `address`        |
| `block.difficulty`       | Difficulty of the current block.                                                              | `uint`           |
| `block.gaslimit`         | Gas limit of the current block.                                                           | `uint`           |
| `block.chainid`          | Chain ID where the contract is running (available since Solidity 0.8.0).        | `uint`           |
| `block.basefee`          | Base gas fee of the block (available since Solidity 0.8.7).                           | `uint`           |
| `gasleft()`              | Amount of gas remaining in the current transaction.                                         | `uint`           |
| `tx.gasprice`            | Gas price of the transaction.                                                          | `uint`           |
| `tx.origin`              | Address of the account that initiated the transaction (similar to `msg.sender` but broader). | `address`        |
| `blockhash(blockNumber)` | Returns the hash of the block given as an argument (only for the 256 most recent blocks). | `bytes32`        |

```solidity
function showInfo() public view returns (address, uint256) {
    return (msg.sender, block.timestamp);
}
```

* `msg.sender`: Provides the address of the function call sender.
* `block.timestamp`: Shows the current block time, useful for time-dependent functions.
