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

# Inheritance

**Inheritance** in Solidity is like a "legacy" that one contract leaves to another. Imagine you have a base contract with a series of functions and data, and then you create another contract that inherits all that content, adding its own functions and data. This allows you to reuse code, make contracts more organized, and even create more complex structures with multiple layers of functionality.

### What is inheritance?

Inheritance in Solidity allows a "child" contract to inherit the properties and functions of a "parent" contract. It's like inheriting your grandmother's cooking talent but then adding your personal touch. In technical terms, the child contract can use functions and variables from the parent contract, and can also modify or extend them.

**Basic syntax:**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Parent {
    // Functions and variables of the parent contract
}

contract Child is Parent {
    // Additional functions and variables of the child contract
}
```

In this example, the `Child` contract inherits all the content from `Parent`, and can also have its own logic.

### Practical Example: Base Contract and Inherited Contract

Let's say we have a base contract that handles a list of products, and we want to create an inherited contract that manages a store with those products:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Base contract that defines products
contract Products {
    struct Product {
        string name;
        uint price;
    }

    Product[] public productList;

    // Function to add products to the list
    function addProduct(string memory _name, uint _price) public {
        productList.push(Product(_name, _price));
    }

    // Function to get the number of products
    function getNumberOfProducts() public view returns (uint) {
        return productList.length;
    }
}

// Contract that inherits from Products and adds store functionality
contract Store is Products {
    mapping(address => mapping(uint => uint)) public cart;

    // Function to add a product to the cart
    function addToCart(uint _productIndex, uint _quantity) public {
        require(_productIndex < productList.length, "Product does not exist");
        cart[msg.sender][_productIndex] += _quantity;
    }

    // Function to view a user's cart
    function viewCart(address _user, uint _productIndex) public view returns (uint) {
        return cart[_user][_productIndex];
    }
}
```

#### How does this contract work?

1. **`Products` Contract**: Defines a `struct` for products and basic functions to add and count products. This contract acts as the base that contains the product list.
2. **`Store` Contract**: Inherits all content from `Products` and adds additional functionality, like a shopping cart managed with a double mapping (`cart`). This mapping stores the quantity of products that each user has in their cart.

### Advantages of using inheritance

1. **Code reuse**: You can avoid duplicating common functions and data across multiple contracts, making your code cleaner and easier to maintain.
2. **Modularity**: You can build complex functionalities in layers, where each contract adds or modifies specific behaviors.
3. **Ease of expansion**: If you need to add new features, you can simply create a new contract that inherits from another, without needing to modify the base contract.

### The `super` keyword

If you ever need a function in the child contract to call the same function in the parent contract, you can use the `super` keyword. This is useful when you want to extend the behavior of a function rather than completely replace it.

For a function to be called or modified in a child contract, it must be marked as `virtual` in the parent contract, and then as `override` in the child contract.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Parent {
    function sayHello() public pure virtual returns (string memory) {
        return "Hello from the parent contract!";
    }
}

contract Child is Parent {
    function sayHello() public pure override returns (string memory) {
        return string(abi.encodePacked(super.sayHello(), " And hello from the child contract!"));
    }
}
```

In this example, `sayHello` in the child contract calls `sayHello` from the parent contract using `super`, and then adds its own message. The result is a combination of both greetings.

### Multiple inheritance

Solidity also allows multiple inheritance, which means a contract can inherit from several contracts at once. This sounds great, but you need to be careful with something called the "Diamond Problem," where multiple parent contracts might have the same function, creating ambiguity. Solidity handles this using a linearization order that defines which contract takes priority.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract A {
    function foo() public pure virtual returns (string memory) {
        return "A";
    }
}

contract B is A {
    function foo() public pure virtual override returns (string memory) {
        return "B";
    }
}

contract C is A {
    function foo() public pure virtual override returns (string memory) {
        return "C";
    }
}

contract D is B, C {
    function foo() public pure override(B, C) returns (string memory) {
        return super.foo(); // Calls foo() from C because C is at the end of the inheritance order
    }
}
```

In this example, contract `D` inherits from both `B` and `C`, but `foo` in `D` calls `C`'s implementation due to the linearization order.

### What happens when there's a constructor?

If the parent contract has a constructor with parameters, you must pass those parameters from the child contract's constructor. This ensures that the parent contract is initialized correctly before the child begins executing its logic.

Let's say you have a parent contract with a constructor that initializes a `name` variable:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Parent {
    string public name;

    constructor(string memory _name) {
        name = _name;
    }
}

contract Child is Parent {
    uint8 public age;

    // Child contract constructor, which calls the parent constructor
    constructor(string memory _name, uint8 _age) Parent(_name) {
        age = _age;
    }
}
```

In this example:

* The `Parent` contract has a constructor that receives a string `_name`.
* The `Child` contract inherits from `Parent` and also has its own constructor, which receives a string `_name` and a uint `_age`.
* In the line `Parent(_name)`, the `Child` contract's constructor calls the `Parent` contract's constructor, ensuring that `name` is initialized correctly before the `Child` contract sets its own `age` variable.

### Multiple inheritance with constructors

If a contract inherits from multiple parent contracts that have constructors, you must specify how to call each of them. Let's see an example:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract A {
    uint8 public x;

    constructor(uint8 _x) {
        x = _x;
    }
}

contract B {
    uint8 public y;

    constructor(uint8 _y) {
        y = _y;
    }
}

contract C is A, B {
    // Calls constructors of A and B
    constructor(uint8 _x, uint8 _y) A(_x) B(_y) {}
}
```

In this case, contract `C` inherits from `A` and `B`, both with constructors that require parameters. The constructor of `C` specifies how to call each of them: `A(_x)` and `B(_y)`. This ensures that both parent contracts are initialized correctly before `C` continues.

