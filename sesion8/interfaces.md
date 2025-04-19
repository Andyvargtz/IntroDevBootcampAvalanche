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

# Interfaces

**Interfaces** in Solidity are like abstract contracts that only define the shape of functions, without implementing their logic. Think of them as an instruction manual for different contracts to know how to communicate with each other. An interface establishes the rules of the game, stating which functions must exist and how they should be called, but not how they behave.

### What is an interface?

An interface is a special contract in Solidity that declares functions without a body. It only defines the function names, their parameters, and what type of data they should return, but they don't contain any internal logic. Any contract that implements this interface must define the logic for these functions.

**Basic syntax:**

```solidity
interface InterfaceName {
    function functionName(parameterType) external view returns (returnType);
}
```

For example, an interface that defines a token contract might look like this:

```solidity
interface ERC20 {
    function totalSupply() external view returns (uint256);
    function balanceOf(address account) external view returns (uint256);
    function transfer(address recipient, uint256 amount) external returns (bool);
}
```

In this example, the `ERC20` interface defines three functions that any ERC20 token contract should have: `totalSupply` for the total token supply, `balanceOf` to get an account's balance, and `transfer` to transfer tokens from one account to another.

In interfaces, functions must be declared as `external`.

### Why use interfaces?

Interfaces are super useful when you need different contracts to interact with each other in a standardized way. By using an interface, you ensure that a contract meets certain minimum requirements so that another contract can interact with it without problems. It's like saying, "if this contract implements this interface, I know I can call it this way."

### Implementing an interface

When a contract implements an interface, it commits to defining all the functions that the interface declares. If you forget any function, your contract won't compile.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Define the interface
interface VehicleRegistry {
    function registerVehicle(string memory _plate, string memory _model) external;
    function getVehicle(string memory _plate) external view returns (string memory model);
}

// Implement the interface in a contract
contract MyVehicleRegistry is VehicleRegistry {
    struct Vehicle {
        string model;
    }

    mapping(string => Vehicle) private vehicles;

    // Implement the function to register a vehicle
    function registerVehicle(string memory _plate, string memory _model) public override {
        vehicles[_plate] = Vehicle(_model);
    }

    // Implement the function to get vehicle data
    function getVehicle(string memory _plate) public view override returns (string memory model) {
        return vehicles[_plate].model;
    }
}
```

In this example:

* The `VehicleRegistry` interface defines two functions: `registerVehicle` and `getVehicle`.
* The `MyVehicleRegistry` contract implements these functions with its own logic to manage a vehicle registry.

### Things you should know about interfaces

1. **You can't have functions with logic**: Functions in an interface can only be declared, not implemented.
2. **You can't have state variables**: Interfaces cannot have variables, constructors, or any type of storage.
3. **You can't inherit from contracts**: Interfaces can only inherit from other interfaces, not from complete contracts.
