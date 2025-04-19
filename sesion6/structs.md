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

# Structs

**Structs** in Solidity allow you to combine different types of data and keep them together. Instead of managing a bunch of loose variables, structs let you group related data into a single package. This is useful when you have an entity that needs to store multiple types of information, such as a user profile or transaction details.

### What is a struct?

A `struct` allows you to define your own data type composed of multiple variables. Each of these variables can be of a different type, such as numbers, addresses, booleans, etc. It's like creating your own template to group related data under a single name.

**Basic syntax:**

```solidity
struct StructName {
    dataType1 variable1;
    dataType2 variable2;
    dataType3 variable3;
}
```

For example, let's say we want to store user information in our contract:

```solidity
struct User {
    string name;
    uint age;
    address wallet;
}
```

Here, the `User` struct groups three variables: `name` (string), `age` (integer), and `wallet` (address). Instead of managing these three pieces of data separately, you can now use them as a single set.

### How to use structs

Once you have defined a struct, you can use it to declare variables that follow that "template". Let's see how it's done:

```solidity
User public user1;
```

Now, `user1` is a variable of type `User` that can store a name, age, and wallet address. You can assign values to each field of the struct like this:

```solidity
user1 = User("Alice", 30, 0x1234567890123456789012345678901234567890);
```

You can also access the values inside the struct using the dot notation:

```solidity
string memory userName = user1.name; // Access the name
user1.age = 31; // Modify the age
```

### Practical example: User System

Let's see how you could use structs to create a system that registers users in a contract:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract UserRegistry {
    // We define the User struct
    struct User {
        string name;
        uint age;
        address wallet;
    }

    // We create a mapping to store users using their address
    mapping(address => User) users;

    // Function to register a new user
    function registerUser(string memory _name, uint _age) public {
        users[msg.sender] = User(_name, _age, msg.sender);
    }

    // Function to get user information
    function getUser(address _wallet) public view returns (string memory, uint, address) {
        User memory user = users[_wallet];
        return (user.name, user.age, user.wallet);
    }
}
```

In this example, we use a `User` struct to group the name, age, and wallet address of users. Then, with the `users` mapping, we store each user's information under their wallet address. Users can register using the `registerUser` function, and you can query any user's data with `getUser`.

### Things you should know about structs

1. **Storage in structs**: Structs can be stored in both **memory** and **storage**. If you declare a struct inside a function, you must specify whether it will be in memory or storage, because Solidity needs to know where to place it.
2. **Gas efficient usage**: Structs can save space by grouping data, but if not optimized properly, they can occupy multiple storage slots, which will increase the gas needed for their manipulation.
3. **Arrays of structs**: You can use arrays of structs to handle multiple instances of the same type. For example, you could have an array of `User[]` if you need to manage a list of users.
4. **Nested structs**: It's also possible to have structs inside other structs. This is useful when you need to organize even more complex data.
