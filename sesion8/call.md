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

# Call

The `call` method in Solidity allows you to send data to any contract using its address, unlike using an interface, regardless of whether you know its structure or not. It's super powerful, but it must be used with care because, as Uncle Ben says, "with great power comes great responsibility."

### What is `call`?

The `call` method is a low-level function used to make calls to other contracts or to send ether to an address. It allows you to call any function of an external contract using its address, even if you don't have the contract's interface or ABI. However, it's a bit risky since it doesn't verify if the function exists or if the parameters are correct, which can lead to errors.

**Basic syntax:**

```solidity
(bool success, bytes memory data) = address.call{value: amount}(abi.encodeWithSignature("functionName(parameters)"));
```

* `success` is a boolean indicating if the call was successful.
* `data` contains the data returned by the called function.
* `address` is the address of the contract you're calling.
* `abi.encodeWithSignature` encodes the function signature and its parameters.

### Calling another function with `call`

Let's imagine we want to call a `setMessage` function in an external contract that changes the stored message. Here's the code:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CallInteraction {
    // Function to call another function in an external contract using `call`
    function changeMessage(address contractAddress, string memory newMessage) public {
        // Create the signature of the function we want to call
        (bool success, bytes memory data) = contractAddress.call(
            abi.encodeWithSignature("setMessage(string)", newMessage)
        );
        
        // Verify if the call was successful
        require(success, "Function call failed");
    }
}
```

In this example:

1. **Call construction**: We use `abi.encodeWithSignature` to create the signature of the function we want to call. The signature includes the function name `setMessage` and its parameter `(string)`.
2. **Call with `call`**: Then, we pass this signature to the `call` method along with the contract address (`contractAddress`) and the message we want to send (`newMessage`).
3. **Result verification**: If `success` is `true`, the call was successful. If not, the transaction fails with the message "Function call failed".

### Advantages and disadvantages of `call`

**Advantages:**

1. **Total flexibility**: You can call any function of any contract, regardless of its structure.
2. **Ether sending**: Allows you to send ether and execute functions in a single step.
3. **Compatibility**: Works even if you don't have the contract's interface, as long as you know the function signature.

**Disadvantages:**

1. **No function existence verification**: If the signature is incorrect or the function doesn't exist, `call` will simply return `false` and the transaction won't do anything useful.
2. **No automatic transaction reversion**: Unlike `transfer` or `send`, `call` doesn't automatically revert the entire transaction if it fails, unless you use `require` or `assert` to verify its success.
3. **Higher security risk**: Since `call` doesn't validate the function you're calling, it's easier to make mistakes that could be exploited by malicious actors.

### Other ways to interact with contracts

Although `call` is incredibly useful, it's not the only way to interact with contracts. You can also use `delegatecall` to execute another contract's code in your contract's context, or `staticcall` to make read-only calls without modifying the state. Each has its specific purpose and its own security implications.
