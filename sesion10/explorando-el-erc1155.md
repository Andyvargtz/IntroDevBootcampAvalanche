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

# Exploring ERC1155

**ERC1155** is an Ethereum standard that defines a set of functions and events for creating and managing multiple types of tokens in a single contract. Unlike the ERC20 and ERC721 standards, **ERC1155** allows both fungible (interchangeable) and non-fungible (unique) tokens under the same contract, which optimizes gas costs and simplifies the storage and transfer of these tokens.

### Key Components of ERC1155

The **ERC1155** standard defines several essential functions and events that all token contracts must implement:

**1. Main functions:**

1. **`constructor`:** Initializes the contract by setting a base URI for all token types. The base URI uses a token `id` substitution mechanism, allowing each token to point to its corresponding metadata.
   * **Parameters:** `uri_` (base URI of the tokens, where `{id}` will be replaced by the specific token ID).
   * **Example**: [`ipfs://QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json`](https://ipfs.io/ipfs/QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json)
2. **`uri(uint256 id)`**: Returns the URI for a specific token type. The URI uses `{id}` as a placeholder that will be replaced by the token identifier in compatible applications.
   * **Parameter**: `id` (unique identifier of the token type).
   * **Returns**: The token's URI as a string.
3. **`balanceOf(address account, uint256 id)`**: Returns the balance of tokens of a specific type for a given address.
   * **Parameter:** `account` (the address to query).
   * **Returns:** The number of tokens owned by that address (uint256).
4. **`balanceOfBatch(address[] memory accounts, uint256[] memory ids)`**: Returns the balance of multiple token types for multiple addresses in a single call.
   * **Parameters**: `accounts` (addresses to query) and `ids` (token type identifiers).
   * **Returns**: An array with the balances corresponding to each address and token type.
5. **`setApprovalForAll(address operator, bool approved)`**: Allows or revokes authorization for another address to handle all of the owner's tokens.
   * **Parameters**: `operator` (address to authorize) and `approved` (whether to authorize or revoke).
   * **Returns**: `true` if the operation is successful.
6. **`isApprovedForAll(address owner, address operator)`**: Verifies if an address is authorized to handle all tokens of an owner.
   * **Parameters**: `owner` (token owner) and `operator` (address to verify).
   * **Returns**: `true` if the address has permission to handle all tokens.
7. **`safeTransferFrom(address from, address to, uint256 id, uint256 value, bytes memory data)`**: Transfers a specific amount of tokens of one type from one address to another.
   * **Parameters**: `from`, `to`, `id`, `value`, and `data` (additional data, optional).
   * **Requirements**: `from` must have sufficient token balance and `to` must not be the zero address.
8. **`safeBatchTransferFrom(address from, address to, uint256[] memory ids, uint256[] memory values, bytes memory data)`**: Transfers multiple token types in a single operation.
   * **Parameters**: `from`, `to`, `ids`, `values`, and `data`.
   * **Requirements**: `from` must have sufficient balance of each token type in `ids`.
9. **\_setURI(string memory newuri)**: Internal function that sets a new URI for all token types, applying the `id` substitution mechanism.
   * **Parameter**: `newuri` (new base URI).
10. **`_mint(address to, uint256 id, uint256 value, bytes memory data)`**: Creates a specific amount of tokens of a given type and assigns them to an address.
    * **Parameters**: `to`, `id`, `value`, and `data`.
    * **Requirements**: `to` must not be the zero address
11. **`_mintBatch(address to, uint256[] memory ids, uint256[] memory values, bytes memory data)`**: Creates multiple token types in a single call and assigns them to an address.
    * **Parameters**: `to`, `ids`, `values`, and `data`.
12. **`_burn(address from, uint256 id, uint256 value)`**: Destroys a specific amount of tokens of one type for a given address.
    * **Parameters**: `from`, `id`, `value`.
13. **`_burnBatch(address from, uint256[] memory ids, uint256[] values)`**: Destroys multiple token types in a single call.
    * **Parameters**: `from`, `ids`, and `values`.

**2. Main events:**

1. **`TransferSingle(address indexed operator, address indexed from, address indexed to, uint256 id, uint256 value)`**: Emitted each time a single token type is transferred from one address to another.
2. **`TransferBatch(address indexed operator, address indexed from, address indexed to, uint256[] ids, uint256[] values)`**: Emitted when multiple token types are transferred in a single operation.
3. **`ApprovalForAll(address indexed account, address indexed operator, bool approved)`**: Emitted when an address allows or revokes token handling to an operator.

### Why is ERC1155 so important?

* **Gas Cost Efficiency**: By grouping multiple token types in a single contract, **ERC1155** reduces gas costs, especially when performing batch transfers.
* **Flexibility**: Supports both fungible and non-fungible tokens in the same contract, making it ideal for applications like video games, where players can have multiple assets (coins, unique items, etc.).
* **Simplified Management**: By using a common structure for various token types, **ERC1155** allows for simpler and more efficient management of large amounts of digital assets.

### Example of ERC1155 Contract

Here's a basic example of an ERC1155 contract using OpenZeppelin:

```solidity
// SPDX-License-Identifier: MIT
import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";

contract MyMultiToken is ERC1155 {
    constructor() ERC1155("ipfs://QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json") {}

    function mint(address account, uint256 id, uint256 amount, bytes memory data) public {
        _mint(account, id, amount, data);
    }

    function mintBatch(address to, uint256[] memory ids, uint256[] memory amounts, bytes memory data) public {
        _mintBatch(to, ids, amounts, data);
    }
}
```

* **Import**: The ERC1155 contract from OpenZeppelin is imported, ensuring all standard rules are followed.
* **Base URI**: When implementing `ERC1155`, a URI is set that includes `{id}`, which will be replaced with the corresponding token's `id` in each URI request.
