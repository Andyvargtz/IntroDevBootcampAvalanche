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

# Default Values

In Solidity, each data type has a **default value** when you declare a variable but don't initialize it. It's like when you buy a t-shirt online and it comes in "one size fits all" by default (although sometimes that doesn't fit anyone).

**Default values** ensure that your variables won't be empty or "broken" when you declare them but forget to initialize them. Solidity will always assign them a safe value so your contract doesn't crash due to missing data. So, if you didn't bother to give something an initial value, Solidity will do it for you!

### What are these default values?

Here's the quick list so you always know what to expect when a variable doesn't have an assigned value:

* **uint (unsigned integers)**: The default value is 0. There are no negative numbers, so it always starts from 0.
* **int (signed integers)**: They also start at 0, but here you can have both positive and negative numbers, although initially you'll have a neutral 0.
* **bool (booleans)**: Here the default value is `false`. So if you don't say anything, a boolean variable always starts as "false".
* **address (addresses)**: Uninitialized addresses will be `0x0000000000000000000000000000000000000000`. Yes, that whole series of zeros is the default value.
* **bytes and strings**: These types are a bit more unusual. Empty `bytes` and `string` have default values that are equivalent to empty sequences (like an empty string `""` or `0x` for `bytes`).

```solidity
uint256 public number; // By default will be 0
bool public state;    // By default will be false
address public address; // By default will be 0x0000000000000000000000000000000000000000
string public name; // By default will be ""
bytes public data; // By default will be 0x
```
