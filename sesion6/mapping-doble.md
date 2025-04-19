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

# Double Mapping

If a mapping already seems great to you, wait until you learn about **double mappings**. They are the perfect tool for situations where you need to store more complex information, such as access permissions, categorized data, or anything that needs two levels of organization.

### What is a double mapping?

A **double mapping** is simply a mapping inside another mapping. Imagine you have a wardrobe (first mapping) and, inside each drawer, you have another smaller wardrobe (second mapping). This way, you can store data in two levels of keys.

**Basic syntax:**

```solidity
mapping(keyType1 => mapping(keyType2 => valueType)) public mappingName;
```

For example, let's say you want to keep track of permissions per user and per application:

```solidity
mapping(address => mapping(string => bool)) public permissions;
```

In this case, `permissions` takes two keys:

1. An address (`address`) to identify the user.
2. A string (`string`) to identify the application.

The stored value is a boolean (`bool`) that indicates whether that user has permission or not for that specific application.

### Practical example of double mapping

Let's see an example where we store and query access permissions:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PermissionSystem {
    // Double mapping: user => (application => permission)
    mapping(address => mapping(string => bool)) public permissions;

    // Function to assign permissions to a user for a specific application
    function assignPermission(address user, string memory application, bool hasPermission) public {
        permissions[user][application] = hasPermission;
    }

    // Function to check if a user has permission for a specific application
    function checkPermission(address user, string memory application) public view returns (bool) {
        return permissions[user][application];
    }
}
</code></pre>

In this contract, each user (`address`) has an associated mapping that stores permissions for different applications (`string`). With the `assignPermission` function, you can grant or revoke permissions, and with `checkPermission` you can verify if a user has access to a specific application. Let's visualize how this would look in a table:

| **User (address)** | **Application** | **Permission** |
| ------------------ | --------------- | -------------- |
| 0x123...abc        | "Facebook"      | true           |
| 0x123...abc        | "Twitter"       | false          |
| 0x456...def        | "Instagram"     | true           |
| 0x789...ghi        | "Facebook"      | false          |

In this table, the first user (`0x123...abc`) has permission to use "Facebook" but not "Twitter". While the second user (`0x456...def`) has access to "Instagram" and the third (`0x789...ghi`) doesn't have permission for "Facebook".

### Advantages of double mappings

1. **Level-based organization**: Perfect for scenarios where you need multiple levels of data, such as users and permissions, categories and subcategories, etc.
2. **Quick and efficient access**: Despite having two levels, accessing a value is fast because Solidity knows how to navigate these mappings.
3. **Flexibility**: You can add or remove permissions without worrying about the contract's structure; you simply update the corresponding mapping.
