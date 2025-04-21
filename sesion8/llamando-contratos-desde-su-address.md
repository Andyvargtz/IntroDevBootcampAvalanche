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

# Calling Contracts from their Address

In Solidity, **calling contracts from their address** is like using someone's phone number to ask them to do something. You have the contract's address and, with that, you can call it to execute a specific function or even interact with its internal logic. This allows different contracts to communicate with each other efficiently and modularly.

### How does it work?

If you know a contract's address and what functions it has, you can easily interact with that contract using an interface. This allows you to make calls to external contracts without needing to copy their code, which is ideal if you only need to use some of their functions.

**Step by step:**

1. **Define the contract interface** with the functions you need to use.
2. **Convert the address** of the external contract to an interface type.
3. **Call the functions** of the contract through that interface.

### Practical example

Let's say we want to interact with a token contract that follows the ERC20 standard, and its address is `0x1234...`. We want to transfer tokens to a specific account. First, we define the token interface:

```solidity
interface IERC20 {
    function transfer(address recipient, uint256 amount) external returns (bool);
    function balanceOf(address account) external view returns (uint256);
}
```

Then, we use this interface to call the contract from its address:

```solidity
contract TokenInteraction {
    // Function to transfer tokens through the contract address
    function sendTokens(address tokenContract, address recipient, uint256 amount) public {
        // Convert the address to the token interface
        IERC20 token = IERC20(tokenContract);
        
        // Call the transfer function of the token contract
        bool success = token.transfer(recipient, amount);
        
        // Verify if the transfer was successful
        require(success, "Transfer failed");
    }

    // Function to query the balance of an account
    function checkBalance(address tokenContract, address account) public view returns (uint256) {
        // Convert the address to the token interface
        IERC20 token = IERC20(tokenContract);
        
        // Call the balanceOf function of the token contract
        return token.balanceOf(account);
    }
}
```

What's happening here?

1. **`IERC20` Interface**: Defines the `transfer` and `balanceOf` functions, which are the standard functions of ERC20 tokens.
2. **Converting address to interface**: In the `sendTokens` function, we take the token contract's address (`tokenContract`) and "convert" it to the `IERC20` interface. This allows us to interact with the contract using the functions we've defined in the interface.
3. **Calling `transfer`**: Then we call the `transfer` function of the external contract using the interface. If the transfer is successful, the function returns `true`; otherwise, we throw an error with `require`.

### Advantages of using interfaces to call external contracts

1. **Modularity**: You don't need to copy code from other contracts, just define an interface and call the functions you need.
2. **Easy to update**: If the external contract updates its logic but maintains the same interface, your contract will continue working without problems.
3. **Simplicity**: The interface allows you to keep your code clean and easy to understand, as you don't need to handle all the internal logic of the external contract.
