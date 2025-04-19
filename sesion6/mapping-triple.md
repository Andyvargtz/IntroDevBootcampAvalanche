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

# Triple Mapping

Double mappings are great, but **triple mappings** take data organization to another level! It's like having a folder with subfolders, and inside each subfolder, even more folders. With triple mappings you can manage information at three different levels, ideal for more complex cases where you need to have data organized by multiple criteria.

### What is a triple mapping?

A **triple mapping** is simply a mapping inside another mapping, which in turn is inside another mapping. It's like a wardrobe with shelves, and each shelf has drawers, and each drawer has boxes. It sounds complicated, but it's super useful when you need to handle data that depends on three keys.

**Basic syntax:**

```solidity
mapping(keyType1 => mapping(keyType2 => mapping(keyType3 => valueType))) public mappingName;
```

For example, let's say we want to keep track of user access to different application modules on specific days:

```solidity
mapping(address => mapping(string => mapping(string => bool))) public access;
```

Here, `access` takes three keys:

1. An address (`address`) to identify the user.
2. A string (`string`) to identify the module (for example, "Finance", "Users").
3. Another string (`string`) for the specific date in `"YYYY-MM-DD"` format.

The stored value is a boolean (`bool`) that indicates whether the user accessed that module on that specific day.

### Practical example: Access Log

Let's see how this is used with a contract to log user access:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AccessLog {
    // Triple mapping: user => (module => (date => access))
    mapping(address => mapping(string => mapping(string => bool))) public access;

    // Function to log user access to a module on a specific date
    function logAccess(address user, string memory module, string memory date) public {
        access[user][module][date] = true;
    }

    // Function to check if a user accessed a module on a specific date
    function checkAccess(address user, string memory module, string memory date) public view returns (bool) {
        return access[user][module][date];
    }
}
```

In this contract, each user has a mapping that stores modules, and each module has another mapping that stores dates and whether there was access or not. Let's see how this would look in a table:

| **User (address)** | **Module**   | **Date**      | **Access** |
| ------------------ | ------------ | ------------- | ---------- |
| 0x123...abc        | "Finance"    | "2023-09-25"  | true       |
| 0x123...abc        | "Users"      | "2023-09-25"  | false      |
| 0x456...def        | "Finance"    | "2023-09-24"  | true       |
| 0x789...ghi        | "Marketing"  | "2023-09-23"  | false      |

In this table, we can see that the first user (`0x123...abc`) accessed the "Finance" module on September 25, 2023, but not the "Users" module. While the second user (`0x456...def`) accessed "Finance" on September 24, and the third (`0x789...ghi`) did not access the "Marketing" module on September 23.

### Advantages of triple mappings

1. **Extreme organization**: Ideal for very complex data structures, such as multi-level access permissions, categorized transaction history, or any other case where you need to organize data by three criteria.
2. **Quick access**: Although it seems complicated, Solidity accesses the values of a triple mapping efficiently using the three keys.
3. **Total flexibility**: You can add or remove data at any level of the mapping without having to redesign the contract's structure. If you need to add a new module or a new date, you simply add a new entry to the mapping.
