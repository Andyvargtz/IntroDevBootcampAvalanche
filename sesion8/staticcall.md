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

# StaticCall

The `staticcall` method in Solidity is the "read-only" mode for interacting with other contracts. It allows you to query information without changing anything in the contract you're calling, which is great when you only need to retrieve data. Unlike `call`, `staticcall` ensures that the contract's state cannot be modified, even if you try to do so. It's perfect for safe calls where you don't want to worry about accidentally altering something in the external contract.

### What is `staticcall`?

`staticcall` is a low-level function used to make safe calls to other contracts, ensuring that the call cannot alter the state of the contract being called. If the function you're trying to call attempts to make changes (like transferring tokens or modifying a variable), `staticcall` will fail. It's like telling the contract: "I want to know something, but I promise not to touch anything."

**Basic syntax:**

```solidity
(bool success, bytes memory data) = address.staticcall(abi.encodeWithSignature("functionName(parameters)"));
```

* `success` is a boolean indicating if the call was successful.
* `data` contains the data returned by the called function.
* `address` is the address of the contract you're calling.
* `abi.encodeWithSignature` encodes the function signature and its parameters.

### Calling another function with `staticcall`

Let's imagine we want to query a user's token balance in an ERC20 contract without changing anything in the contract. Here's how it's done:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BalanceQuery {
    // Function to query balance using `staticcall`
    function queryBalance(address tokenContract, address account) public view returns (uint256) {
        // Prepare the call with `staticcall`
        (bool success, bytes memory data) = tokenContract.staticcall(
            abi.encodeWithSignature("balanceOf(address)", account)
        );
        
        // Verify if the call was successful
        require(success, "staticcall failed");
        
        // Decode the result to get the balance
        return abi.decode(data, (uint256));
    }
}
```

1. **Call construction**: We use `abi.encodeWithSignature` to create the signature of the `balanceOf` function, which takes an address as a parameter (`account`).
2. **Call with `staticcall`**: We call the `balanceOf` function of the token contract (`tokenContract`) using `staticcall`.
3. **Result verification**: If `success` is `true`, the call was successful. If not, the transaction fails with the message "staticcall failed".
4. **Result decoding**: We use `abi.decode` to convert the returned data (`data`) into an integer (`uint256`), which is the user's balance.

### Advantages and disadvantages of `staticcall`

**Advantages:**

1. **Security**: Ensures no changes will be made to the called contract, protecting against unwanted modifications.
2. **Efficiency**: Read-only calls are cheaper in terms of gas since they don't need to record changes on the blockchain.
3. **Ideal for queries**: Perfect for querying balances, contract states, and any other information that doesn't need to alter the contract.

**Disadvantages:**

1. **Read-only limitation**: You can't do anything that modifies the state, like transferring tokens or updating variables.
2. **Failure in state-changing functions**: If you try to call a function that modifies the state, the call will fail, as `staticcall` doesn't allow changes.

### Comparison with `call` and `delegatecall`

* **`call`**: Allows you to make any type of call, including state changes and sending ether. It's flexible but potentially risky.
* **`delegatecall`**: Executes another contract's code in the context of your contract. Changes your own state instead of the called contract's.
* **`staticcall`**: Is the safe and specific option for read-only calls, ensuring no changes are made to the external contract.

### Why use `staticcall`?

If you only need to query data without affecting the contract's state, `staticcall` is your best option. For example, if you want to verify balances, contract states, or any other static information, `staticcall` guarantees that no unexpected changes will occur. This makes it an essential tool for avoiding errors or unwanted behaviors in your contracts.
