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

# Exploring ERC721

**ERC721** is a standard that defines a set of functions and events for creating and managing NFTs (non-fungible tokens). This standard allows each token to have a unique identifier, differentiating it from other tokens and ensuring its individuality. Think of ERC721 as a set of rules that allow NFTs to function uniformly in applications, wallets, and marketplaces, ensuring that all non-fungible tokens speak the same "language".

### Key Components of ERC721

The **ERC721** standard defines several essential functions and events that all token contracts must implement:

**1. Main functions:**

1. **`constructor`:** Sets the name and symbol of the token when the contract is deployed. These values are immutable and cannot be changed after creation.
   * **Parameters:** `name_` (token name) and `symbol_` (token symbol).
   * **Example**: If you create a token with `constructor("MyUniqueToken", "MUT")`, the name will be "MyUniqueToken" and the symbol "MUT".
2. **`name()`:** Returns the name of the token. It's a read-only function and its value is set during contract construction.
   * **Returns:** The token name as a string (`string`).
3. **`symbol()`:** Returns the token symbol, usually an abbreviation or short version of the name.
   * **Returns:** The token symbol (`string`).
4. **`tokenURI(uint256 tokenId)`**: Provides a link (URI) to the token's metadata, which typically includes information such as name, description, and images.
   * **Parameter**: `tokenId` (unique token identifier).
   * **Returns**: The URI (string) pointing to the token's metadata.
5. **\_baseURI()**: Internal function that sets the base URI for all tokens.
   * **Returns**: The base URI (string) for tokens, can be overridden in inherited contracts.
6. **`balanceOf(address account)`:** Returns the number of tokens owned by a specific address.
   * **Parameter:** `account` (the address to query).
   * **Returns:** The number of tokens owned by that address (uint256).
7. **`ownerOf(uint256 tokenId)`:** Returns the address that owns a specific token.
   * **Parameter:** `tokenId` (token identifier).
   * **Returns:** The owner's address (address).
8. **`safeTransferFrom(address from, address to, uint256 tokenId)`**: Safely transfers a token from the owner to another address.
   * **Parameters:** `from` (current owner's address), `to` (recipient's address) and `tokenId` (identifier of the token to transfer).
   * **Requirements:** The sender must own the token or have the owner's approval.
   * **Returns:** `true` if the transfer was successful.
9. **`approve(address to, uint256 tokenId)`**: Authorizes another address to transfer a token on behalf of the owner.
   * **Parameters**: `to` (authorized address) and `tokenId` (token identifier).
   * **Returns**: `true` if the approval is successful.
10. **`setApprovalForAll(address operator, bool approved)`**: Allows or revokes authorization for another address to handle all of the owner's tokens.
    * **Parameters**: `operator` (address to authorize) and `approved` (whether to authorize or revoke).
    * **Returns**: `true` if the operation is successful.
11. **`getApproved(uint256 tokenId)`**: Returns the address authorized to transfer a specific token.
    * **Parameter**: `tokenId` (token identifier).
    * **Returns**: Authorized address (address).
12. **`isApprovedForAll(address owner, address operator)`**: Verifies if an address is authorized to handle all tokens of an owner.
    * **Parameters**: `owner` (token owner) and `operator` (address to verify).
    * **Returns**: `true` if the address has permission to handle all tokens.
13. **`_isAuthorized(address owner, address spender, uint256 tokenId)`**: Verifies if an address is authorized to handle a specific token.
    * **Parameters**: `owner`, `spender`, `tokenId`.
    * **Returns**: `true` if the address has authorization.
14. **`_checkAuthorized(address owner, address spender, uint256 tokenId)`**: Verifies and reverts if an address is not authorized to handle a token.
    * **Parameters**: `owner`, `spender`, `tokenId`.
    * **Use**: Prevents unauthorized actions on the token.
15. **`_update(address to, uint256 tokenId, address auth)`**: Transfers `tokenId` to `to` or performs minting/burning if applicable.
    * **Parameters**: `to`, `tokenId`, `auth`.
    * **Returns**: The previous owner.
16. **`_safeMint(address to, uint256 tokenId)`**: Safe version of `_mint` that verifies recipient acceptance.
    * **Parameter:** `account` (address to which tokens are assigned) and `value` (amount of tokens created).
17. **`_burn(address account, uint256 value)`**: Destroys tokens from the specified account, reducing the total token supply.
    * **Parameters**: `to`, `tokenId`.
18. **`_safeMint(address to, uint256 tokenId)`**: Safe version of `_mint` that verifies recipient acceptance.
    * **Parameters**: `to`, `tokenId`.
19. **`_burn(uint256 tokenId)`**: Destroys a token and clears its ownership.
    * **Parameter**: `tokenId`.

**2. Main events:**

1. **`Transfer(address indexed from, address indexed to, uint256 indexed tokenId)`**: Emitted every time a token is transferred from one address to another.
2. **Approval(address indexed owner, address indexed approved, uint256 indexed tokenId)**: Emitted when the owner of a token authorizes another address to transfer the token.
3. **ApprovalForAll(address indexed owner, address indexed operator, bool approved)**: Emitted when the owner allows or revokes authorization for an operator to handle all their tokens.

### Why is ERC721 so important?

* **Interoperability**: By standardizing functions, ERC721-based NFTs can be transferred and used in any wallet or platform that supports this standard.
* **Uniqueness and Authenticity**: Each ERC721 token is unique, making it an excellent choice for representing exclusive digital assets or collectibles.
* **Permission Management**: With functions like `approve` and `setApprovalForAll`, ERC721 allows granular control of ownership and delegation of transfer permissions.

### ERC721 Contract

Here's how a basic ERC721 contract would look using OpenZeppelin, a library that simplifies the implementation of secure and standard contracts:

```solidity
// We import the ERC721 contract from OpenZeppelin
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

// We create an ERC721 contract called "NFTCollection"
contract NFTCollection is ERC721 {
    constructor() ERC721("NFTCollection", "CNFT") {}

    function mintNFT(address recipient, uint256 tokenId) public {
        _safeMint(recipient, tokenId);
    }
}
```

* **Import**: The standard ERC721 implementation from OpenZeppelin is imported, ensuring all standard rules are followed.
* **Token Creation**: A token called "NFTCollection" is initialized with the symbol "CNFT". This contract allows minting new NFTs safely and assigning them to a specific address with `mintNFT`.
