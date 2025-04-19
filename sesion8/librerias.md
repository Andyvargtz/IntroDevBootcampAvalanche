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

# Libraries

In Solidity, **libraries** work similarly to contracts, but they are optimized to not take up extra space on the blockchain and to not be deployed by themselves. Instead of creating multiple copies of a function in each contract, you can use a library to centralize the logic and have multiple contracts reuse it. This saves gas and keeps the code cleaner and more efficient.

### What is a library?

A library in Solidity is a set of functions that can be used by other contracts. Libraries cannot maintain state, meaning they don't have state variables and cannot receive ether. They are designed to be lightweight and modular, and can be defined as "internal" or "external", depending on how you want to use them.

* **Internal**: The library functions are copied into the calling contract during compilation. No additional address is required to invoke them.
* **External**: The library is deployed as a separate contract and then contracts call its functions through the library's address, which reduces storage space.

### How does a library work?

A library can contain functions that apply to specific data types or more general functions that other contracts can invoke. The big advantage is that they allow code reuse and make your contracts more modular.

**Basic library syntax:**

```solidity
library MyLibrary {
    function increment(uint value) internal pure returns (uint) {
        return value + 1;
    }
}
```

This is a simple example of a library called `MyLibrary` with an `increment` function that takes a number and increases it by one. This function can be used by other contracts to reuse this logic, instead of writing it repeatedly.

### String library

Let's look at a more interesting example. We'll create a library that works with strings, allowing them to be converted to uppercase.

```solidity
library StringUtils {
    // Converts a string to uppercase
    function toUpperCase(string memory str) internal pure returns (string memory) {
        bytes memory bStr = bytes(str);
        for (uint i = 0; i < bStr.length; i++) {
            if (bStr[i] >= 0x61 && bStr[i] <= 0x7A) {
                bStr[i] = bytes1(uint8(bStr[i]) - 32);
            }
        }
        return string(bStr);
    }
}
```

**What does this library do?**

1. **Converts strings**: The `toUpperCase` function converts any lowercase letter in a string to uppercase.
2. **Reusable**: This logic can be used in any contract that needs to manipulate strings.

### Using the library in a contract

Once we have defined the library, we can use it in any contract. Here's how to do it:

```solidity
import "./StringUtils.sol";

contract StringManager {
    using StringUtils for string;

    // Returns a string in uppercase
    function convert(string memory text) public pure returns (string memory) {
        return text.toUpperCase();
    }
}
```

In this example, we're using the `StringUtils` library to convert a string to uppercase. The line `using StringUtils for string` allows us to extend the `string` type and use the `toUpperCase` function as if it were part of the basic string functions.

### Considerations when using libraries

* **Pure and view functions**: Because libraries have no state, the functions they contain are usually pure (`pure`) or read-only (`view`), meaning they cannot modify the contract's state.
* **Not independent contracts**: Libraries cannot be deployed by themselves, but they can be called by other contracts to execute logic.
* **Security**: Using audited or well-tested libraries improves the security of your contracts, as you reduce the risk of introducing errors or vulnerabilities.
