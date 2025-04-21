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

# Exploring ERC20

### What is ERC20?

ERC20 is a standard that defines a common set of functions and events that all tokens must implement to be compatible with most applications and wallets. Think of it as a communication protocol that ensures all tokens speak the same "language", allowing them to be easily transferred, exchanged and managed.

{% embed url="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol" %}

### Key Components of ERC20

The ERC20 standard defines six fundamental functions and two events that all token contracts must implement:

**1. Main functions:**

1. **`constructor`:** Sets the name and symbol of the token when the contract is deployed. These values are immutable and cannot be changed after creation.
   * **Parameters:** `name_` (token name) and `symbol_` (token symbol).
   * **Example:** If you create a token with `constructor("MyToken", "MTK")`, the name will be "MyToken" and the symbol "MTK".
2. **`name()`:** Returns the name of the token. It's a read-only function and its value is set during contract construction.
   * **Returns:** The token name as a string (`string`).
3. **`symbol()`:** Returns the token symbol, usually an abbreviation or short version of the name.
   * **Returns:** The token symbol (`string`).
4. **`decimals()`:** Returns the number of decimals used by the token for its representation. By default, it's 18, which means 1 token is divided into 10^18 parts.
   * **Returns:** An integer (`uint8`) representing the decimals.
5. **`totalSupply()`:** Shows the total amount of tokens in circulation. This value changes only when tokens are created or destroyed (through `_mint` or `_burn`).
   * **Returns:** The total amount of tokens in existence (`uint256`).
6. **`balanceOf(address account)`:** Returns the token balance of a specific address. Allows checking how many tokens a particular account owns.
   * **Parameter:** `account` (the address to query).
   * **Returns:** The token balance in the address (`uint256`).
7. `transfer(address to, uint256 value)`: Transfers a specific amount of tokens from the sender to another address.
   * **Parameters:** `to` (recipient's address) and `value` (amount of tokens to transfer).
   * **Requirements:** The sender must have at least `value` tokens.
   * **Returns:** `true` if the transfer was successful.
8. `allowance(address owner, address spender)`: Shows the amount of tokens that an owner has allowed a third party (spender) to spend on their behalf.
   * **Parameters:** `owner` (token owner) and `spender` (who has permission to spend).
   * **Returns:** Amount of allowed tokens (`uint256`).
9. `approve(address spender, uint256 value)`: Authorizes another address to spend a specific amount of your tokens. Useful for allowing automated contracts to make payments on your behalf.
   * **Parameters:** `spender` (authorized address) and `value` (amount of allowed tokens).
   * **Returns:** `true` if the approval was successful.
10. `transferFrom(address from, address to, uint256 value)`: Allows transferring tokens from one account to another on behalf of someone else, as long as it has been previously approved.
    * **Parameters:** `from` (source address), `to` (destination address) and `value` (amount of tokens to transfer).
    * **Requirements:** `from` must have enough tokens and the sender must have permission to spend at least `value` tokens.
    * **Returns:** `true` if the transfer was successful.
11. `_transfer(address from, address to, uint256 value)`: Internal function that moves tokens from one address to another. This function is called by `transfer` and `transferFrom`.
    * **Parameters:** `from` (source of tokens), `to` (destination of tokens) and `value` (amount of tokens transferred).
12. `_update(address from, address to, uint256 value)`: Updates account balances during a transfer, minting or burning. If `from` is the zero address, a new amount of tokens is created. It's possible to override this function to add custom logic, such as additional restrictions or specific events.
13. `_mint(address account, uint256 value)`: Creates new tokens and assigns them to the specified account. Increases the total token supply.
    * **Parameter:** `account` (address to which tokens are assigned) and `value` (amount of tokens created).
14. `_burn(address account, uint256 value)`: Destroys tokens from the specified account, reducing the total token supply.
    * **Parameter:** `account` (address from which tokens are removed) and `value` (amount of tokens destroyed).
15. `_approve(address owner, address spender, uint256 value, bool emitEvent)`: Sets a specific amount of tokens that a `spender` can spend on behalf of `owner`. If `emitEvent` is true, it emits an `Approval` event.
    * **Parameters:** `owner` (token owner), `spender` (who has permission to spend), `value` (amount of allowed tokens) and `emitEvent` (whether to emit an event).
16. `_spendAllowance(address owner, address spender, uint256 value)`: Updates the amount of tokens that a `spender` can spend on behalf of `owner` based on the spent value. Does not update the value if the allowed amount is maximum (`type(uint256).max`).
    * **Parameters:** `owner` (token owner), `spender` (who has permission to spend), `value` (amount spent).

**2. Main events:**

1. **`Transfer(address indexed from, address indexed to, uint256 value)`**: Triggered every time tokens are transferred, whether directly between two users or through `transferFrom`. It's how block explorers and third-party applications track token movements.
2. **`Approval(address indexed owner, address indexed spender, uint256 value)`**: Emitted when the owner approves a third party to spend their tokens. It's like leaving a paper trail of who has permission to spend what amount of tokens.

### Why is ERC20 so important?

1. **Interoperability:** Any dApp (decentralized application) that supports ERC20 tokens can interact with any token that follows this standard, without needing to know specific implementation details. This facilitates the creation of exchanges, wallets and DeFi platforms.
2. **Standardization:** Thanks to all ERC20 tokens working the same way, it's easy to integrate new tokens into existing platforms. For example, adding a new token to an ERC20-compatible wallet is as simple as adding its contract address.
3. **Security and reliability:** The standard reduces the possibility of errors and vulnerabilities because it follows established and tested rules. Although not infallible, using ERC20 helps avoid many common problems in smart contract creation.

### ERC20 Contract

Here's how a basic ERC20 contract would look using OpenZeppelin, a library that simplifies the implementation of secure and standard contracts:

```solidity
// We import the ERC20 contract from OpenZeppelin
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

// We create an ERC20 contract called "TokenSimple"
contract TokenSimple is ERC20 {
    constructor(uint256 initialSupply) ERC20("TokenSimple", "TS") {
        _mint(msg.sender, initialSupply);
    }
}
```

1. **Import:** The standard ERC20 implementation from OpenZeppelin is imported, ensuring all standard rules are followed.
2. **Token Creation:** A token called `TokenSimple` is initialized with the symbol `TS`, and an initial amount of tokens is assigned to the contract creator.
