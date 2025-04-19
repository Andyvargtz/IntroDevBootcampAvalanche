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

# Modifiers

**Modifiers** in Solidity are like little guardians of functions, responsible for verifying that certain conditions are met before the code executes. Think of them as a filter that decides whether the function continues or not. They are super useful for avoiding code repetition and ensuring that certain functions only execute under specific circumstances.

### What is a modifier?

A `modifier` is a piece of code that you can apply to a function to add additional logic. It's like putting a lock on the function, and the modifier is the key that verifies if you have permission to enter or not. They are defined with the `modifier` keyword and, like functions, can receive parameters.

**Basic syntax:**

```solidity
modifier modifierName() {
    // Logic before executing the function
    _;
    // Logic after executing the function (optional)
}
```

The word `_` (underscore) indicates where the rest of the function that uses the modifier will execute. You can place it before, after, or even surround it with code if you want to execute logic before and after the function.

For example:

<pre class="language-solidity"><code class="lang-solidity">modifier onlyOwner() {
    require(msg.sender == owner, "You are not the owner");
<strong>    _;
</strong>}
</code></pre>

### Practical example: Only the Owner

Let's imagine a contract where only the owner can execute certain functions. We define an `onlyOwner` modifier that verifies if the caller is the owner of the contract:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract OnlyOwner {
</strong>    address owner = 0x1234567890123456789012345678901234567890;
   
    // Modifier to verify if the caller is the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "You are not the owner");
        _;
    }

    // Function protected with the modifier
    function changeOwner(address newOwner) public onlyOwner {
        owner = newOwner;
    }

    // Function only for the owner
    function ownerOnlyFunction() public onlyOwner {
        // Code exclusive to the owner
    }
}
</code></pre>

Here, the `onlyOwner` modifier checks that `msg.sender` (the address calling the function) is equal to `owner`. If it's not, the transaction fails with the message "You are not the owner".

### What are modifiers used for?

1. **Code reuse**: Instead of writing the same validation logic in each function, you can create a modifier and apply it to all functions that need that logic.
2. **Improves readability**: By having the logic separated in modifiers, functions become cleaner and easier to read.
3. **Access control**: Modifiers are perfect for restricting who can execute a function, when it can be executed, or under what conditions.

### Modifiers with parameters

Modifiers can also receive parameters to make the validation more specific. For example, you can verify that a function can only be executed after a specific date:

```solidity
modifier onlyAfter(uint time) {
    require(block.timestamp >= time, "You cannot execute this function yet");
    _;
}

function executeAfter(uint _time) public onlyAfter(_time) {
    // Code that only executes after the specified time
}
```

In this case, `onlyAfter` checks that the current time (`block.timestamp`) is greater than or equal to the time specified as a parameter. If it's not, the function doesn't execute.

### Practical example: Advanced access control

Let's imagine a contract where funds are managed, and only administrators can withdraw money after a specific date:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SecureFund {
    address public administrator;
    uint public unlockDate;

    constructor() {
        administrator = msg.sender;
        unlockDate = block.timestamp + 30 days; // Locked for 30 days
    }

    // Modifier to verify administrator and unlock date
    modifier onlyAdministratorAfter() {
        require(msg.sender == administrator, "You are not the administrator");
        require(block.timestamp >= unlockDate, "Funds locked until unlock date");
        _;
    }

    // Protected function to withdraw funds
    function withdrawFunds(uint amount) public onlyAdministratorAfter {
        // Code to withdraw funds
    }
}
```

Here, `onlyAdministratorAfter` ensures that only the administrator can withdraw funds and only after the unlock date. This prevents withdrawals before the time and by unauthorized people.

### Things to keep in mind with modifiers

1. **They require gas**: Modifiers, like any other logic, consume gas. Make sure their use is justified and doesn't unnecessarily increase transaction costs.
2. **Don't abuse them**: Although they are useful, having too many modifiers can make your code difficult to follow. Use modifiers when they truly add clarity and efficiency.
3. **Cleanup logic**: If you need to execute logic before and after the function, make sure the modifier's structure clearly reflects the flow you want.
