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

# Creating our first contract

You already know the initial structure of a contract. Now, we are going to create our first simple smart contract. This time I will give you the code and all you have to do is copy and paste it. Don't worry if you don't understand anything about the code yet, in the following sections we will explain everything step by step.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MyFirstContract {

    string message;

    function sendMessage(string memory _newMessage) public {
        mensaje = _newMessage;
    }

    function readMessage() public view returns(string memory){
        return message;
    }
}
```

This contract has two functions:

* `sendMessage`: Updates the value of the message variable.
* `readMessage`: Shows the current value of the message variable.

The `message` variable is of type `string`, which means it is a character string, that is, a text.

When trying to paste this code into your contract, you will get the following warning:

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

This is because Remix asks you to be careful that the source from which you got the code is secure and trustworthy, because there could be the possibility of interacting with malicious code that drains all your funds.
