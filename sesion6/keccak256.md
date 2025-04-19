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

# Keccak256

The **keccak256** algorithm is a hashing function that takes any amount of data and converts it into a unique 32-byte (256-bit) value. It's super useful for ensuring that data isn't modified and for avoiding collisions (two different inputs generating the same hash). It's the digital equivalent of putting an entire cake into a shredder and getting a unique code - no matter how hard you try, you can't reconstruct the original cake just from that code.

Keccak256 ensures that any change, no matter how small, in the original data will produce a completely different hash. This makes it the perfect tool for comparing, validating, and securing information in smart contracts.

### The problem with `strings` and how `keccak256` solves it

Imagine you want to verify if two strings are equal, something like checking if `"Hello"` is equal to `"hello"`. In Solidity, you can't simply do `if (string1 == string2)`, because strings can't be compared that way directly. This is because Solidity doesn't have a comparison operator for `strings`. So, what do you do?

This is where **keccak256** comes to the rescue. What you do is convert both strings into their corresponding hash using `keccak256` and then compare those hashes. If the hashes are equal, then the strings are too.

```solidity
function compareStrings(string memory _a, string memory _b) public pure returns (bool) {
    return keccak256(abi.encodePacked(_a)) == keccak256(abi.encodePacked(_b));
}
```

In this code, both strings are converted into their hash using `keccak256` and compared. This ensures that any variation in the strings, no matter how small, will result in different hashes.

### Other uses of `keccak256`

The use of `keccak256` goes far beyond comparing strings. Here are some examples of how it can be used in different contexts:

1. **Create unique identifiers**: If you need a unique identifier for something in your contract, like a wallet address or a token, `keccak256` is perfect. You can use it to generate an identifier from multiple combined data, such as the user's address, a random number, and a timestamp.

    {% code fullWidth="false" %}
    ```solidity
    function generateID(address _user, uint _timestamp) public pure returns (bytes32) {
        return keccak256(abi.encodePacked(_user, _timestamp));
    }
    ```
    {% endcode %}
2. **Verify digital signatures**: In contracts where you need to verify the authenticity of a signature, `keccak256` is used to create the hash of the signed message. This hash is then compared with the provided signature to ensure it hasn't been altered.
3. **Generate pseudo-random numbers**: Although Solidity doesn't have a random number function as such, you can use `keccak256` with unpredictable data (like `block.timestamp` and `block.difficulty`) to create something similar. But be careful, it's not really secure for important things like gambling.

    ```solidity
    function randomNumber(uint256 _input) public view returns (uint256) {
        return uint256(keccak256(abi.encodePacked(block.timestamp, block.difficulty, _input)));
    }
    ```

### How does `keccak256` work under the hood?

Under the surface, `keccak256` uses a hashing algorithm that transforms the input into data blocks and performs mathematical and logical operations to generate the final hash. Every bit in the input affects the resulting hash, and changing even a single character in the input will produce a completely different hash. This makes it ideal for detecting changes in data and protecting against manipulations.
