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

# Import

In Solidity, the `import` command is like opening a toolbox and taking out exactly what you need. It allows you to reuse code from other files in your own contract, keeping your project organized and avoiding unnecessary duplication. Essentially, with `import` you can bring in contracts, libraries, or interfaces from other files, which is especially useful in large projects where each contract or library is in its own file.

### How does `import` work?

The `import` command allows you to include the content of another file in your current contract. You can think of it as a way to "copy and paste" all the code from an external file, but without having to do it manually. This facilitates the reuse of existing contracts and libraries, and allows you to separate logic into different files to keep everything organized.

**Basic syntax:**

```solidity
import "path/file.sol";
```

The path can be relative (within your project) or absolute (if you're using NPM packages or OpenZeppelin libraries, for example).

### Basic example of `import`

Let's say you have a math library in a file called `Math.sol`, and you want to use its functions in your main contract. Your project structure would look something like this:

```markdown
- contracts/
  - Math.sol
  - MyContract.sol
```

1. **Content of `Math.sol` file:**

```solidity
// Basic math library
library Math {
    function add(uint a, uint b) internal pure returns (uint) {
        return a + b;
    }

    function subtract(uint a, uint b) internal pure returns (uint) {
        return a - b;
    }
}
```

2. **Content of `MyContract.sol` file:**

```solidity
// Import the Math library
import "./Math.sol";

contract MyContract {
    // Use the Math library in our contract
    function calculateSum(uint a, uint b) public pure returns (uint) {
        return Math.add(a, b); // Call to the library's add function
    }

    function calculateSubtract(uint a, uint b) public pure returns (uint) {
        return Math.subtract(a, b); // Call to the library's subtract function
    }
}
```

#### What's happening here?

1. **Importing `Math.sol`:** The `MyContract` contract imports the `Math` library from the `Math.sol` file using the relative path `./Math.sol`.
2. **Using library functions:** Inside `MyContract`, we call the `add` and `subtract` functions from the `Math` library without needing to redefine them. This keeps our code clean and modular.

### Other ways to use `import`

1. **Import all content from a file:**

    ```solidity
    import "./Utils.sol";
    ```

    This imports all content from `Utils.sol` into your contract.
2. **Import with alias:** You can assign aliases to avoid name conflicts when importing multiple libraries or contracts with similar names.

    ```solidity
    import { Math as MathLib } from "./Math.sol";
    ```

    Now you can use `MathLib.add(a, b)` instead of `Math.add(a, b)`.
3. **Import only specific elements:** If you only need certain functions or contracts from a large file, you can import them individually.

    ```solidity
    import { add, subtract } from "./Math.sol";
    ```

    Now only `add` and `subtract` are available in your contract.

### Using external libraries

One of the great advantages of `import` is the ability to use third-party contracts and libraries. For example, you can use OpenZeppelin libraries to implement security functions, role management, or standard ERC20 and ERC721 contracts.

**Example:**

```solidity
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 1000 * 10 ** decimals());
    }
}
```

In this example:

* We're importing the `ERC20` contract from the OpenZeppelin library.
* The `MyToken` contract inherits from `ERC20` and leverages all the functionality implemented by OpenZeppelin to create a standard ERC20 token.

### Important considerations when using `import`

1. **Avoid cyclic imports:** Make sure two files don't import each other, as this will cause compilation errors.
2. **Control versions:** Ensure that the versions of imported files are compatible with your contract to avoid compilation or execution issues.
3. **Maintain organization:** Using `import` effectively can make your code much more manageable and modular. Organize your contracts and libraries in logical folders to facilitate their use.
