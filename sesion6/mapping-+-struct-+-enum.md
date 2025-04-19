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

# Mapping + Struct + Enum

Let's combine the best of three worlds! When you use **mappings**, **structs**, and **enums** together in Solidity, you can organize super complex data in an orderly and efficient way. It's like putting together a puzzle where each piece has its place and purpose. This combination is ideal for applications that need to manage data with multiple levels of information and logic.

### How does the combination work?

1. **Mapping**: Helps you associate keys with values. It can be a user with their information, a product with its price, or any other combination of data.
2. **Struct**: Groups different types of data into a single container. Think of a user profile that has a name, age, and address, all in one "package".
3. **Enum**: Defines a set of predefined options, like contract states (Active, Inactive, Suspended) or access levels (User, Administrator).

### Practical example: Task Management

Let's imagine we want to create a system to manage tasks, where each task has a state and is assigned to a user. We'll use an `enum` to define the task state, a `struct` to store the task details, and a `mapping` to organize all tasks by user.

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TaskManagement {
    // Define the enum for task states
    enum TaskState { Pending, InProgress, Completed }

    // Create a struct to represent a task
    struct Task {
        string description;
        TaskState state;
        uint creationDate;
    }

    // Mapping from user to a list of tasks
    mapping(address => Task[]) userTasks;

    // Function to create a new task
    function createTask(string memory _description) public {
        Task memory newTask = Task(_description, TaskState.Pending, block.timestamp);
        userTasks[msg.sender].push(newTask);
    }

    // Function to update the state of a specific task
    function updateTaskState(uint index, TaskState newState) public {
        require(index < userTasks[msg.sender].length, "Task index out of range");
        userTasks[msg.sender][index].state = newState;
    }

    // Function to get the details of a specific task
    function getTask(address user, uint index) public view returns (string memory, TaskState, uint) {
        Task memory task = userTasks[user][index];
        return (task.description, task.state, task.creationDate);
    }
}
</code></pre>

1. **Enum `TaskState`**: Defines three possible states for each task: `Pending`, `InProgress`, and `Completed`.
2. **Struct `Task`**: Groups the task description, its state, and creation date into a single package.
3. **Mapping `userTasks`**: Associates each user address (`address`) with an array of `Task` structs, allowing each user to have their own task list.

### Contract interaction:

* Users can **create tasks** with `createTask`, which adds a new task to their list.
* They can **update the state** of a specific task with `updateTaskState`, changing its state to `InProgress` or `Completed`.
* The `getTask` function allows you to **query the details** of a specific task from any user, returning its description, state, and creation date.

### Example in practice:

Let's say Alice creates two tasks and manages them as follows:

1. **Create task**:
   * `description`: "Buy supplies"
   * `state`: `Pending`
   * `creationDate`: `1696015200` (timestamp)
2. **Update state**:
   * Task 1: Changes to `InProgress`.
   * Task 2: Changes to `Completed`.

After these operations, the data structure in the `userTasks` mapping for Alice would look something like this:

| **User** | **Index** | **Description**     | **State** | **Creation Date** |
| ----------- | ---------- | ------------------- | ---------- | --------------------- |
| 0x123...abc | 0          | Buy supplies | InProgress | 1696015200            |
| 0x123...abc | 1          | Submit reports   | Completed | 1696015300            |
