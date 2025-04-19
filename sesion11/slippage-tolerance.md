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

# Slippage Tolerance

**Slippage Tolerance** is a crucial concept in decentralized exchanges (DEX) and automated market makers (AMM). It refers to the maximum percentage difference between the expected price of a trade and the actual execution price that a user is willing to accept. Understanding and setting an appropriate slippage tolerance is essential for successful trading in the DeFi space.

### **What is Slippage?**

Slippage occurs when the execution price of a trade differs from the expected price at the time the trade was initiated. This difference can be due to various factors, including market volatility, liquidity depth, and the size of the trade relative to the available liquidity in the pool.

### **How Slippage Tolerance Works**

When you place a trade on a DEX, you can set a slippage tolerance percentage. This percentage represents the maximum amount by which the execution price can differ from the expected price before the trade is automatically canceled. For example, if you set a slippage tolerance of 1%, and the price moves more than 1% between the time you submit the trade and when it is executed, the trade will not go through.

### **Setting Slippage Tolerance**

Setting the right slippage tolerance is a balance between ensuring your trade executes and protecting yourself from unfavorable price movements. Here are some considerations:

* **Low Slippage Tolerance (e.g., 0.1% - 0.5%)**: Suitable for highly liquid pairs with stable prices. This setting minimizes the risk of significant price changes but may result in failed trades if the market is volatile.
* **Medium Slippage Tolerance (e.g., 1% - 2%)**: A common setting for most trades, offering a good balance between execution success and price protection.
* **High Slippage Tolerance (e.g., 3% or more)**: Used for less liquid pairs or during periods of high volatility. This increases the chance of trade execution but also the risk of receiving a less favorable price.

### **Factors Affecting Slippage**

Several factors can influence the amount of slippage you experience:

* **Liquidity Depth**: Pools with more liquidity generally have lower slippage because larger trades can be executed without significantly affecting the price.
* **Trade Size**: Larger trades relative to the pool's liquidity will cause more slippage.
* **Market Volatility**: High volatility can lead to rapid price changes, increasing the likelihood of slippage.
* **Network Congestion**: During times of high network activity, transactions may take longer to process, increasing the chance of price changes between submission and execution.

### **Example of Slippage**

Suppose you want to swap 1 ETH for USDC on a DEX. The current price is 1 ETH = 3,000 USDC, and you set a slippage tolerance of 1%. If the price moves to 1 ETH = 2,970 USDC (a 1% decrease) by the time your trade executes, it will still go through. However, if the price drops to 1 ETH = 2,940 USDC (a 2% decrease), your trade would be canceled if your slippage tolerance is set to 1%.

### **Managing Slippage in Your Trades**

To minimize slippage and improve your trading experience, consider the following tips:

* **Use Limit Orders**: Some DEXs offer limit orders, allowing you to set a specific price at which you want your trade to execute.
* **Split Large Trades**: For large trades, consider splitting them into smaller orders to reduce the impact on the market price.
* **Monitor Market Conditions**: Be aware of current market conditions and adjust your slippage tolerance accordingly.
* **Choose High-Liquidity Pools**: Trading in pools with higher liquidity can help reduce slippage.
