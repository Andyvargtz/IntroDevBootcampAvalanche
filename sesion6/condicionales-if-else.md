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

# If / Else Conditionals

**`if / else` conditionals** in Solidity are control structures that allow executing different blocks of code depending on whether a condition is met or not. Basically, they are the "if this happens, do this, otherwise, do that" of programming.

### How does it work?

In short, `if` evaluates a condition. If that condition is true, it executes the corresponding block of code. If not, you can add an `else` to tell the contract what to do otherwise. Let's go with examples to make it clearer.

**Basic `if` example:**

```solidity
function checkNumber(uint256 number) public pure returns (string memory) {
    if (number > 10) {
        return "The number is greater than 10";
    }
    // There's no else here, so if the condition is not met, nothing happens.
}
```

In this case, the function checks if the number is greater than 10. If it is, it returns the message "The number is greater than 10". If it's not, it simply does nothing (or you can add an `else` if you want to handle that situation).

### What if I want to add more options?

If you need to control more than one condition, you can use `else` or even `else if` to check multiple scenarios. This allows you to handle several possibilities without complicating your life.

**`if/else` example:**

```solidity
function checkAge(uint256 age) public pure returns (string memory) {
    if (age >= 18) {
        return "You are of legal age";
    } else {
        return "You are underage";
    }
}
```

Here the function returns whether someone is of legal age or underage, depending on the value of `age`. But if you want to handle more options, use `else if`.

**Example with `else if`:**

```solidity
function checkScore(uint256 points) public pure returns (string memory) {
    if (points > 100) {
        return "You won the grand prize";
    } else if (points > 50) {
        return "You get the second prize";
    } else {
        return "Keep participating";
    }
}
```

With `else if`, you're adding an additional condition. If you don't win the grand prize but have more than 50 points, you still get something!
