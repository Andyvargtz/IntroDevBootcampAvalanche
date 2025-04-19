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

# Data Types

When working with smart contracts in Solidity, **data types** are the foundation of everything. They are the way you define and structure information within your contract. Through them, you can control everything from simple numbers and text strings to complex structures and data collections.

A data type is how you define what kind of value a variable can have. Just as in real life we have different ways of representing information (numbers, words, lists), in Solidity we have different data types to define how that information is stored and managed within the contract.

### Main data types in Solidity

1. **Integers (int and uint)**: Integers are one of the most basic data types in any programming language, and Solidity is no exception. There are two main types:
   * **int**: Represents integers that can be positive or negative. You can define the size of the integer by specifying the number of bits it occupies (for example, `int8`, `int16`, `int256`). If you don't specify, the default value is `int256`.
   * **uint**: Represents unsigned integers, that is, only positive numbers. As with `int`, you can specify the size of the integer (`uint8`, `uint16`, `uint256`). The default value is `uint256`.
   *   **Storage considerations**: Data is stored in 32-byte slots, so if you use several small integers (like `uint8` and `uint16`) within the same slot, you optimize space usage. However, if you use a `uint256` alongside small integers, that `uint256` will occupy a complete slot, and the small integers will be placed in another slot, wasting space.

       ```solidity
       uint8 a = 1; // 1 byte
       uint32 b = 2; // 4 bytes
       uint256 c = 3; // 32 bytes
       ```
2.  **Booleans (bool)**: Boolean data types can only have two values: `true` or `false`. They are extremely useful when you need to define conditions or restrictions in your contract.

    * **Gas considerations**: Although a boolean only needs 1 bit to store its value, in Solidity it occupies a **complete byte**.

    <pre class="language-solidity"><code class="lang-solidity"><strong>bool public isValid = true;
    </strong></code></pre>
3.  **Address (address)**: `address` types are used to store account addresses on the blockchain. An address can be that of a user or another smart contract, and it is used to send and receive ether, grant access control, or to interact with other contracts.

    ```solidity
    address owner = 0x5a4e9Bb1f224e8254C1d63e90dE34E8572f8dC71; // 20 bytes
    ```

    Additionally, Solidity has a special type called `address payable` that allows sending ether to that address.
4.  **String and Bytes**:

    * **string**: Used to store text strings. For example, names or descriptions. Unlike other languages, string operations in Solidity are limited due to their high cost in terms of gas.
    * **bytes**: Are sequences of bytes of fixed or variable length. The `bytes` and `bytes1`, `bytes2`, ..., `bytes32` types are more efficient than `string` for storing binary data or encoded information.
    * **Gas considerations**: Manipulating long strings or dynamic `bytes` variables is expensive. Whenever possible, use fixed-length `bytes` for operations that don't require dynamic size changes.

    ```solidity
    string public name = "Blockchain";
    bytes32 public hash = keccak256(abi.encodePacked(name)); // 32 bytes
    ```



Each byte of storage on the blockchain has a cost. Using the most appropriate data types and structuring them efficiently not only makes your contract cheaper to deploy and execute, but also minimizes the possibility of costly errors. Additionally, by optimizing storage, you improve contract performance and reduce gas costs for you and your users.

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

* **First slot**:
  * **Small variables (`uint8`, `uint16`, `bool`)**: They are grouped to occupy only one slot, which has a capacity of 32 bytes. Here they occupy a total of 26 bytes, making good use of the space.
  * **Address (`address`)**: This type occupies 20 bytes, sharing the slot with other small variables.
* **Second and third slot**:
  * **`uint256` and `int256`**: Each of these variables occupies a complete slot of 32 bytes, as they are of fixed and maximum size (256 bits).
* **Fourth slot**:
  * **`bytes32`**: This data type occupies 32 fixed bytes, which is ideal for storing identifiers or hashes. Here it is used to store the identifier "Blockchain!".
* **Fifth slot**:
  * **`string`**: `string`s are dynamic and occupy more than one slot. In the first slot, a hash is stored that points to the actual content of the text string, which is stored in other storage slots.
* **Sixth slot**:
  * **`bool` and `uint8`**: These small variables are grouped to optimize space usage. There are still 30 bytes available in this slot, which means you could add more small variables without needing to use a new slot.
