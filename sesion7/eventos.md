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

# Events

**Events** in Solidity are like those shouts of "Hey, something happened here!" that allow you to communicate from smart contracts to the outside. Imagine you're organizing a party and want to notify everyone when someone arrives, when the food is ready, or when the music changes. Each of those notifications is like an event, informing those outside the contract about what's happening inside.

### What is an event?

An event in Solidity is a way to record important data on the blockchain that can be queried later without needing to spend gas. Events allow a contract to emit messages that are captured by decentralized applications (dApps) or other contracts to react to specific changes or actions.

```solidity
event EventName(dataType indexed variableName, dataType variableName);
```

For example, if you're managing an auction and want to notify when someone makes a new bid, you could define an event like this:

```solidity
event NewBid(address indexed bidder, uint amount);
```

Here, `NewBid` is the name of the event that records the bidder's address and the amount offered. The word `indexed` makes that parameter easier to search, like a tag.

To emit an event, you simply need to call its name and pass it the parameters you defined. It's like throwing a message into the air, but it's only heard on the blockchain.

### **Example of use in a contract:**

```solidity
contract Auction {
    // Define the event for new bids
    event NewBid(address indexed bidder, uint amount);

    // Function to make a bid in the auction
    function makeBid(uint _amount) public {
        // Logic to handle the bid...
        
        // Emit the event to notify the new bid
        emit NewBid(msg.sender, _amount);
    }
}
```

Every time someone calls `makeBid`, the contract emits the `NewBid` event, recording who made the bid and how much they offered. This is stored in the blockchain logs and can be queried by any dApp interested in following the auction.

### What are events used for?

1. **Historical record:** Events allow you to create a history of what happens inside the contract, like a diary of all important actions.
2. **Communication with dApps:** dApps can listen to events to update their interface or perform automatic actions in response.
3. **Reduction of gas costs:** Data stored in events is not directly accessible by other contracts, but it's much cheaper than storing it as state variables.

### Practical example: Event in a voting contract

Let's imagine we want to record every time someone votes in an election:

```solidity
contract Voting {
    // Define the event to record votes
    event VoteCast(address indexed voter, string candidate);

    // Function to cast a vote
    function castVote(string memory _candidate) public {
        // Logic to handle the vote...

        // Emit the event to record the vote
        emit VoteCast(msg.sender, _candidate);
    }
}
```

Here, every time someone votes, the `VoteCast` event is emitted with the voter's address and the candidate's name. This data is not only recorded on the blockchain, but any dApp can use it to show real-time results or execute additional logic.

### Things you should know about events

1. **They are not accessible within the contract:** Although events are recorded on the blockchain, you cannot access them from other contracts. They serve more as an external communication tool.
2. **Data limit:** Events have a data limit of 32 bytes per parameter, so you can't send very large data. If you need to store a lot of information, it's better to use regular storage in the contract.
3. **`indexed` and its magic:** You can mark up to three parameters of an event as `indexed`. This allows you to easily search and filter those events on the blockchain, like hashtags on social networks.
4. **Gas costs:** Emitting an event costs gas, but it's much cheaper than storing the same data directly in the contract.
