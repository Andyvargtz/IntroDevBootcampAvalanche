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

# Constructor

The **constructor** in Solidity is that initial moment where you define how your contract will be configured. It's responsible for putting everything in place from the start. It only executes once, at the moment of contract deployment, and is perfect for setting initial variables, assigning roles, or configuring any value you don't want to change later.

### What is a constructor?

A constructor is a special function that has the same name as the contract (in older versions of Solidity) or is declared with the `constructor` keyword (in recent versions). It executes automatically when the contract is deployed on the blockchain, and after that, it disappears like a ninja, it cannot be called again or updated.

**Basic syntax:**

```solidity
constructor() {
    // Constructor logic
}
```

For example, if we want to assign the contract creator as the "owner", we can do it in the constructor:

```solidity
contract MyContract {
    address public owner;

    constructor() {
        owner = msg.sender; // Assigns the contract creator as owner
    }
}
```

In this case, `msg.sender` refers to the address that deployed the contract, and the constructor stores it as `owner`.

### What is the constructor used for?

The constructor is perfect for initializing the contract's state and setting important configurations. Some typical things you can do in a constructor include:

1. **Assign owners or roles:** Ideal for contracts where only certain users have special permissions, like administration contracts.
2. **Set initial values:** You can configure limits, fees, or any other value that shouldn't change.
3. **Configure external interactions:** You can initialize external contracts or set up integrations with other contracts or services.

### Practical Example: Registration System

Let's build a contract that uses the constructor to set the owner and a registration cost:

```solidity
contract RegistrationSystem {
    address public owner;
    uint256 public registrationCost;

    // Constructor that sets the owner and registration cost
    constructor(uint256 _registrationCost) {
        owner = msg.sender; // The contract creator is the owner
        registrationCost = _registrationCost; // Sets the initial cost
    }

    // Function to change the registration cost (only the owner can do this)
    function changeRegistrationCost(uint256 newCost) public {
        require(msg.sender == owner, "Only the owner can change the cost.");
        registrationCost = newCost;
    }
}
```

In this contract, the constructor takes a parameter (`_registrationCost`) and uses it to set the initial registration cost. It also sets `msg.sender` as the `owner`. After the contract is deployed, no one else can execute the constructor.

### Things you should know about the constructor

1. **Only executes once:** Once the constructor finishes its execution, it cannot be called again. It's like setting the game rules: once you start playing, you can't change them.
2. **No specific name:** In older versions of Solidity, the constructor had to have the same name as the contract. In current versions, you only need to use the `constructor` keyword.
3. **Limited interactions:** Although you can interact with other contracts within the constructor, keep in mind that any logic that depends on future conditions must be handled carefully, as you won't be able to run the constructor again to fix issues.
4. **No extra gas cost:** Although it executes important logic, the constructor doesn't impose additional gas costs. The cost of deploying the contract already includes the constructor's execution.
