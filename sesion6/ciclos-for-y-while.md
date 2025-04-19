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

# For and While Loops

**For and while loops** are used to repeat a block of code multiple times, but be careful, they're not very gas-friendly. Here I'll explain how they work, when to use them (and when not to), and give you some tips to avoid spending more gas than necessary.

### `for` Loop

The `for` loop is ideal when you know exactly how many times you want something to repeat. It's like saying: "I'm going to iterate over these 10 elements and that's it".

```solidity
function sumElements(uint[] memory numbers) public pure returns (uint) {
    uint sum = 0;
    for (uint i = 0; i < numbers.length; i++) {
        sum += numbers[i];
    }
    return sum;
}
```

In this example, `for` goes through all the elements in the `numbers` list and adds each one to the `sum` variable. Easy, right? But be careful, if the array is too long the gas cost can skyrocket. So before using `for` make sure the size of the list isn't a mystery.

### `while` Loop

The `while` loop repeats a block of code while a condition is true. It's like saying: "I'm going to keep eating pizza until I can't anymore".

**Basic example:**

```solidity
function countdown(uint start) public pure returns (uint) {
    uint counter = start;
    while (counter > 0) {
        counter--;
    }
    return counter;
}
```

Here, `while` keeps subtracting 1 from `counter` until it reaches 0. Useful, but if you're not careful with the condition, you could end up in an infinite loop and use up all the transaction's gas.

### When to use them and when to avoid them?

1. **Don't abuse them**: Loops are useful, but each iteration consumes gas. If your loop depends on user input (like an array of unknown length), you could end up with a transaction that costs a fortune or simply doesn't execute because it runs out of gas.
2. **Prefer `for` over `while`**: In general, the `for` loop is safer because its exit condition is usually more controlled. With `while`, if you forget to update the condition, boom, infinite loop.
3. **Consider splitting the logic**: If you need to go through a huge array, think about splitting the task into multiple transactions or using events to notify progress. It's not as simple as a loop, but it can save you from many headaches.

### Pro Tip: Avoid using loops inside payable functions

Loops can significantly increase a transaction's gas cost. If your function also receives Ether (`payable`), it's not a good idea to put long loops in it. The transaction could fail and the user is left wondering "what happened here?".
