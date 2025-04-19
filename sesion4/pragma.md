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

# Pragma

The `pragma` is a directive that tells the Solidity compiler which version of Solidity should be used to compile the contract. In other words, it's like a "rule" that sets the range of compiler versions in which your code can be safely executed. This is important because different versions of Solidity can have significant changes in their syntax or behavior, and specifying the correct version ensures that your contract works as planned.

The pragma usually goes below the license and its most common format is:

```solidity
pragma solidity ^0.8.18;
```

This line is telling the compiler that it can use any version of Solidity from 0.8.18 onwards, but not greater than the next major version, such as 0.9.0. This allows your code to remain compatible with future minor updates without breaking due to major changes.

There are also other ways to specify the compiler version, although they are not as common:

*   **Fixed version**: If you want your contract to only be compiled with an exact version of Solidity, you can specify a fixed version, as in this example:

    ```solidity
    pragma solidity 0.8.7;
    ```

    This means that your contract can only be compiled with Solidity version 0.8.7. If you try to compile it with a different version, the compiler will throw an error.
*   **Version range**: Instead of using a fixed version, you can allow the contract to be compiled with a range of versions, giving you more flexibility:

    ```solidity
    pragma solidity >=0.7.0 <0.9.0;
    ```

    This pragma indicates that your contract can be compiled with any version of Solidity from 0.7.0 up to any version less than 0.9.0. This way, your code remains compatible with a wider range of compiler versions.

In our case, we will define the pragma in the classic way, and in version 0.8.20 or higher.

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
If you receive an error here, it's probably because the compiler version you have configured in Remix is different from the one you declared in the `pragma`. We'll see how to solve this error later.
{% endhint %}
