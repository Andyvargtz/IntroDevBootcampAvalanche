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

# Mapping + Struct + Enum + Arrays

This is where everything comes together! Combining **mappings**, **structs**, **enums**, and **arrays** helps you build a complex and super-organized structure to handle detailed data. With this mix, you can create complex applications, from a marketplace to a project management system. Each piece has its place, and when you put them together, you get a well-oiled machine that can handle multi-level data and relationships.

### How does this combination work?

1. **Mapping**: It's like an index that helps you associate a key with a value. Ideal for quickly searching for specific information.
2. **Struct**: Allows you to group related data into a single container, like a user profile with their name, age, and address.
3. **Enum**: Defines a limited set of options, like project states or access levels.
4. **Array**: Stores a list of elements of the same type, like a set of tasks or products.

### Practical example: Project Management System

Let's imagine you want to build a system where you can manage projects, each project has different tasks, each task has a state, and each user can be involved in multiple projects. Let's combine mappings, structs, enums, and arrays to achieve this.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ProjectManagement {
    // Enum for task states
    enum TaskState { Pending, InProgress, Completed, Cancelled }

    // Struct to represent a task
    struct Task {
        string description;
        TaskState state;
        uint creationDate;
    }

    // Struct to represent a project
    struct Project {
        string name;
        address leader;
        Task[] tasks;
    }

    // Mapping from user to a list of projects
    mapping(address => Project[]) userProjects;

    // Function to create a new project
    function createProject(string memory _name) public {
        // Create a new project with the name and the leader who creates it
        Project memory newProject;
        newProject.name = _name;
        newProject.leader = msg.sender;
        
        // Add the project to the user's project list
        userProjects[msg.sender].push(newProject);
    }

    // Function to add a new task to a specific project
    function addTask(uint projectIndex, string memory _description) public {
        // Create a new task and add it to the project
        Task memory newTask = Task(_description, TaskState.Pending, block.timestamp);
        userProjects[msg.sender][projectIndex].tasks.push(newTask);
    }

    // Function to update the state of a specific task in a project
    function updateTaskState(uint projectIndex, uint taskIndex, TaskState newState) public {
        // Update the task state
        userProjects[msg.sender][projectIndex].tasks[taskIndex].state = newState;
    }

    // Function to get the details of a specific project
    function getProject(address user, uint projectIndex) public view returns (string memory, address, uint) {
        Project memory project = userProjects[user][projectIndex];
        return (project.name, project.leader, project.tasks.length);
    }

    // Function to get the details of a specific task in a project
    function getTask(address user, uint projectIndex, uint taskIndex) public view returns (string memory, TaskState, uint) {
        Task memory task = userProjects[user][projectIndex].tasks[taskIndex];
        return (task.description, task.state, task.creationDate);
    }
}
```

### How does this contract work?

1. **Enum `TaskState`**: Defines four possible states for each task: `Pending`, `InProgress`, `Completed`, and `Cancelled`.
2. **Struct `Task`**: Groups the task description, its state, and creation date.
3. **Struct `Project`**: Groups the project name, the leader (who created it), and an array of tasks (`Task[]`).
4. **Mapping `userProjects`**: Stores an array of `Project[]` for each user (`address`), allowing each user to have multiple projects.

### Contract interaction:

* Users can **create projects** with `createProject`, assigning it a name and saving it to their project list.
* With `addTask`, you can **add tasks** to a specific project.
* Using `updateTaskState`, you can **change the state** of a task, moving from `Pending` to `InProgress`, `Completed`, or `Cancelled`.
* The `getProject` function allows you to **query details** of a project, such as its name, leader, and number of tasks.
* With `getTask`, you can **query specific details** of a task within a project, including its description, state, and creation date.

### Example in practice:

Let's imagine that Bob creates a project called "App Launch", and adds two tasks:

**Project**: "App Launch"

* **Task 1**: "Design the interface" (Pending)
* **Task 2**: "Create the landing page" (InProgress)

| **User** | **Project**    | **Task Index** | **Description**       | **State** | **Creation Date** |
| ----------- | ------------------ | ---------------- | --------------------- | ---------- | --------------------- |
| 0x456...def | App Launch | 0                | Design the interface   | Pending  | 1696015200            |
| 0x456...def | App Launch | 1                | Create the landing page | InProgress | 1696015400            |
