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

# License

The first thing you encounter when creating a `.sol` file is a warning:

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

This is because Solidity asks you to declare the type of license for the file in the first line of code. By specifying a license, you tell the community what they can do with your contract, whether they can modify it, distribute it, or use it in their own projects.

In other words, the license defines the terms under which your code can be shared or reused by other developers.

### Common types of licenses in Solidity

When writing contracts in Solidity, it is most common to use an **open source** license, which allows other developers to use, modify, and improve your code. Some of the most used licenses in the world of smart contracts are:

1.  **MIT License**: This is one of the most common and permissive licenses. It basically allows anyone to use, copy, modify, and distribute your code, as long as they include a copy of the original copyright notice. It's ideal if you want your code to be completely open.

    ```solidity
    // SPDX-License-Identifier: MIT
    ```
2.  **GPL-3.0 License**: This license is more restrictive than the MIT. It allows others to use and modify your code, but any derivation of your work must maintain the same license. This ensures that the modified code is also open source.

    ```solidity
    // SPDX-License-Identifier: GPL-3.0
    ```
3.  **Unlicense**: If you prefer that your code has no restrictions and is completely public, you can use the **Unlicense**, which allows anyone to do whatever they want with your code, without obligations.

    ```solidity
    // SPDX-License-Identifier: Unlicense
    ```

For the code we are developing, we will use the MIT license, so we will add that code in the first line.

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>
