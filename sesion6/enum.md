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

# Enum

**Enums** in Solidity are lists of options that allow you to handle predefined values in a more readable and organized way. Imagine you have a package delivery application and want to record the package status as "Sent", "In Transit", or "Delivered". Instead of using numbers or text strings, you can use an `enum` to make it clearer and avoid logic errors.

### What is an enum?

An `enum` (short for enumeration) allows you to define a set of possible values that a variable can have. It's like a dropdown menu where you can only choose between the available options, preventing you from entering invalid values.

**Basic syntax:**

```solidity
enum Status { Sent, InTransit, Delivered }
```

Here, `Status` is an `enum` with three possible values: `Sent`, `InTransit`, and `Delivered`. These values are stored internally as integers, starting from 0 (Sent = 0, InTransit = 1, Delivered = 2).

### How are enums used?

Using enums is super simple and allows you to improve code readability. For example, let's say we want to track the status of a package:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PackageDelivery {
    // We define the enum for package statuses
    enum Status { Sent, InTransit, Delivered }

    // State variable to store the current package status
    Status public currentStatus;

    // Function to update the package status
    function updateStatus(Status newStatus) public {
        currentStatus = newStatus;
    }

    // Function to get the current package status as text
    function getStatus() public view returns (string memory) {
        if (currentStatus == Status.Sent) {
            return "The package has been sent.";
        } else if (currentStatus == Status.InTransit) {
            return "The package is in transit.";
        } else {
            return "The package has been delivered.";
        }
    }
}
```

In this contract, `currentStatus` is a variable of type `Status` that can only have one of the predefined values. The `updateStatus` function allows changing the package status, and `getStatus` returns a description of the current status.

### Things you should know about enums

1. **Numbers behind the options**: Each `enum` value has an associated integer starting from 0. So, `Sent` is 0, `InTransit` is 1, and `Delivered` is 2. This is important because you can use these numbers to compare or assign values.
2. **Gas efficient usage**: Since they are internally represented as integers, enums are more gas efficient than using text strings to represent states.
3. **Size limitations**: An `enum` cannot have more than 256 values, as each value is stored in 1 byte. If you need more options, it's better to use a different data structure.
4. **Direct comparison**: You can directly compare the value of an enum with another value of the same enum. This makes logic decisions based on state very clear and easy to follow.

### Practical example with multiple states

Let's see another example where we use an enum to represent the status of a project:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Project {
    // We define the enum for project statuses
    enum Status { Planning, Development, Review, Completed }

    // State variable to store the current project status
    Status public projectStatus;

    // Function to advance to the next project status
    function advanceStatus() public {
        projectStatus = Status(uint(projectStatus) + 1);
    }

    // Function to get the current project status as text
    function getProjectStatus() public view returns (string memory) {
        if (projectStatus == Status.Planning) {
            return "The project is in planning phase.";
        } else if (projectStatus == Status.Development) {
            return "The project is in development.";
        } else if (projectStatus == Status.Review) {
            return "The project is under review.";
        } else {
            return "The project is completed.";
        }
    }
}
```

In this contract, `projectStatus` goes through four states: `Planning`, `Development`, `Review`, and `Completed`. The `advanceStatus` function allows moving to the next status, as long as it's not already in `Completed`.
