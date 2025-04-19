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

# Vesting

**Vesting** is a mechanism used in the cryptocurrency and blockchain world to gradually release tokens or assets to their holders over a specific period. This practice is common in projects and companies that want to ensure long-term commitment from their team members, investors, or advisors.

### **What is Vesting?**

Vesting is a process where tokens or assets are **locked** in a smart contract and are gradually released to their holders according to a predefined schedule. This means that even though someone may own certain tokens, they cannot access or use them immediately, but must wait for the vesting period to complete.

### **How Vesting Works**

The vesting process typically follows these steps:

1. **Token Locking**: Tokens are locked in a smart contract that controls their release.
2. **Vesting Schedule**: A schedule is established that determines when and how many tokens will be released. This can be linear (equal amounts over time) or follow a specific curve.
3. **Release Conditions**: Conditions for token release are defined, which may include time periods, performance milestones, or other criteria.
4. **Gradual Release**: Tokens are gradually released to holders according to the established schedule.

### **Types of Vesting**

There are several types of vesting schedules commonly used:

* **Linear Vesting**: Tokens are released in equal amounts over the vesting period. For example, if 1000 tokens are vested over 12 months, approximately 83.33 tokens would be released each month.
* **Cliff Vesting**: A period during which no tokens are released, followed by a sudden release of a portion of the tokens. After the cliff, tokens may continue to be released linearly.
* **Performance-based Vesting**: Tokens are released based on achieving specific milestones or performance goals.

### **Example of Vesting**

Suppose a startup decides to allocate 1,000,000 tokens to its team with a 4-year vesting period and a 1-year cliff. Here's how it would work:

* **Cliff Period**: During the first year, no tokens are released.
* **After Cliff**: At the end of the first year, 25% of the tokens (250,000) are released.
* **Monthly Releases**: The remaining 750,000 tokens are released linearly over the next 3 years, meaning approximately 20,833 tokens per month.

### **Importance of Vesting**

Vesting is crucial for several reasons:

* **Alignment of Interests**: Ensures that team members and investors are committed to the long-term success of the project.
* **Prevention of Token Dumping**: Prevents large amounts of tokens from being sold immediately, which could negatively impact the token's price.
* **Project Stability**: Provides stability and predictability in token distribution, which is attractive to investors and users.

### **Vesting in Smart Contracts**

Vesting is typically implemented through smart contracts that automatically manage the release of tokens. These contracts are programmed to follow the vesting schedule and release tokens only when the conditions are met. This ensures transparency and trust in the process, as the rules are encoded in the blockchain and cannot be altered without consensus.
