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

# Arrays

**Arrays** in Solidity are lists where you can store collections of data of the same type. Imagine a row of numbered lockers, where each locker can contain a specific value. Whether you need to store a group of numbers, addresses, or any other type of data, arrays allow you to do it in an organized and accessible way.

### What is an array?

An array is a data structure that stores a collection of elements of the same type, either of fixed or dynamic size. Each element has an index, starting from 0, that allows you to access or modify its value easily.

**Basic syntax:**

```solidity
dataType[] public arrayName;
```

For example:

```solidity
uint[] public numbers;
address[] public addresses;
```

In this case, `numbers` is an array of integers (`uint`), while `addresses` is an array of addresses (`address`). Both are dynamic arrays, which means they can grow or shrink in size as elements are added or removed.

### Fixed-size and dynamic arrays

* **Fixed-size array:** Has a specific number of elements that cannot change once defined.

```solidity
uint[3] public top3Numbers = [1, 2, 3]; // Array with 3 fixed elements
```

* **Dynamic array:** Has no predefined limit and its size can change by adding or removing elements.

```solidity
uint[] public numberList; // Dynamic array
```

### Basic operations with arrays

Arrays in Solidity allow you to perform common operations like adding, modifying, deleting, and querying elements. Let's see some examples:

**1. Adding elements to a dynamic array:**

```solidity
numberList.push(10); // Adds the number 10 to the end of the array
```

**2. Accessing and modifying elements:**

```solidity
uint firstNumber = numberList[0]; // Accesses the first element (index 0)
numberList[0] = 20; // Changes the value of the first element to 20
```

**3. Deleting elements (only for dynamic arrays):**

```solidity
numberList.pop(); // Removes the last element from the array
```

**4. Array length:**

```solidity
uint length = numberList.length; // Returns the number of elements in the array
```

### Practical example: Participant List

Let's see an example where we use a dynamic array to manage a list of participants in an event contract:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Event {
    // Dynamic array of addresses
    address[] public participants;

    // Function to add a participant
    function addParticipant(address _participant) public {
        participants.push(_participant);
    }

    // Function to get the total number of participants
    function totalParticipants() public view returns (uint) {
        return participants.length;
    }

    // Function to get a participant by their index
    function getParticipant(uint index) public view returns (address) {
        return participants[index];
    }
}
</code></pre>

In this contract, you can add participant addresses with `addParticipant`, check how many participants there are with `totalParticipants`, and get a specific participant with `getParticipant`.

### Things to keep in mind with arrays

1. **Be careful with indices:** Always make sure the index is within the array's range. Trying to access an index outside the range will result in an error and fail the transaction.
2. **Gas usage:** Operations like `push` and `pop` on dynamic arrays consume gas. Manipulating large arrays can become expensive quickly, so use them in moderation.
3. **No native deletion methods:** Although you can use `.pop()` to remove the last element, there is no native method to delete a specific element and maintain order. To delete intermediate elements, you need custom logic.
