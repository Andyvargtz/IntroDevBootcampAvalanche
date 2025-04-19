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

# Timestamp

The **timestamp** in Solidity is like the blockchain's clock. It allows you to know the exact moment (in seconds since January 1, 1970) when a block was created, a transaction was executed, or a specific action was taken. It's super useful for things like verifying deadlines, setting time limits, or executing functions only at specific times.

### What is a timestamp?

A timestamp is an integer that represents time in seconds since midnight on January 1, 1970, also known as "Unix epoch". In the context of Solidity, the timestamp generally refers to the moment when a block is mined.

```solidity
uint public currentTime = block.timestamp;
```

Here, `block.timestamp` returns the exact moment when the block in which the transaction is being executed was created. This is especially useful for time-dependent functions, such as contracts that have to unlock funds after a certain date or that execute actions only in specific periods.

### Common uses of timestamp in Solidity

1.  **Verify dates**: You can use `block.timestamp` to ensure that a function only executes after a certain time.

    ```solidity
    function releaseFunds() public {
        require(block.timestamp >= releaseDate, "Funds cannot be released yet");
        // Logic to release funds
    }
    ```
2.  **Create timers**: You can also use timestamps to create timers or "cooldowns" in contracts, allowing certain actions to only be executed after a time interval.

    ```solidity
    uint public lastAction;

    function performAction() public {
        require(block.timestamp >= lastAction + 1 days, "You must wait 1 day before performing this action again");
        lastAction = block.timestamp;
        // Action logic
    }
    ```
3.  **Specific events**: If you want an event to occur at a specific time and date, the timestamp is the way to program this logic.

    ```solidity
    function specialEvent() public {
        require(block.timestamp == specificDate, "The event only occurs on a specific date");
        // Special event logic
    }
    ```

### Things to keep in mind with timestamps

1. **They are not 100% accurate**: The timestamp is set by the miner who mines the block, and has a manipulation margin of a few seconds. Although it's usually not a problem for most applications, it's important to keep in mind that you shouldn't use timestamps for things that require absolute precision.
2. **Don't use timestamps to generate random numbers**: Since miners can influence the timestamp value, using it to generate random numbers in the contract can lead to manipulable and insecure results.
3. **Time conversions**: Solidity doesn't have date and time functions like standard programming libraries, so you'll have to do all the conversions manually (seconds, minutes, hours, days).

### Practical example: Auction Contract with Timestamp

Let's see how a timestamp is used in a simple auction contract. The auction only allows bids during a specific time period:

```solidity
contract Auction {
    address public highestBidder;
    uint public highestBid;
    uint public auctionStart;
    uint public auctionEnd;

    constructor(uint _auctionDuration) {
        auctionStart = block.timestamp;
        auctionEnd = auctionStart + _auctionDuration;
    }

    function bid() public payable {
        require(block.timestamp >= auctionStart, "The auction has not started");
        require(block.timestamp <= auctionEnd, "The auction has ended");
        require(msg.value > highestBid, "Your bid must be higher than the current bid");

        if (highestBidder != address(0)) {
            payable(highestBidder).transfer(highestBid); // Refunds the previous highest bidder
        }

        highestBidder = msg.sender;
        highestBid = msg.value;
    }

    function claimFunds() public {
        require(block.timestamp > auctionEnd, "The auction has not ended yet");
        require(msg.sender == highestBidder, "Only the highest bidder can claim the funds");
        payable(highestBidder).transfer(highestBid);
    }
}
```

In this auction contract:

1. **Constructor**: Defines the auction's start and end time.
2. **`bid` function**: Only allows bids during the auction time.
3. **`claimFunds` function**: Allows the auction winner to claim the funds after the auction has ended.
