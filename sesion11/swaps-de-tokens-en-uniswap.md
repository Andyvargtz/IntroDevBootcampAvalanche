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

# Token Swaps on Uniswap

**Token swapping** is one of the main functions of Uniswap, allowing users to exchange one token for another in a decentralized manner without intermediaries. This mechanism is key to Uniswap's operation, as it facilitates exchanges quickly, securely, and accessibly for any user, regardless of their experience in the cryptocurrency market.

### **What is a Token Swap?**

The swap in Uniswap allows users to exchange one ERC-20 token for another using liquidity pools. Each swap follows the constant product formula **(x \* y = k)** to determine the exchange price, adjusting the value of tokens based on supply and demand within the pool.

A swap is executed through a **smart contract**, where the user sends an amount of token A to the contract and receives in return an amount of token B, based on the current ratio in the pool and taking into account the exchange fee.

### **Performing a Token Swap on Uniswap**

1. **Access the Uniswap Platform**: Visit Uniswap and connect your wallet (MetaMask or Core) to interact with the platform.
2. **Select the Swap Function**: On the main Uniswap page, or select the "Swap" tab, where you can choose the tokens you want to exchange.
3.  **Choose the Tokens**: Select the token you want to exchange (for example, **ETH**) and the token you want to receive (for example, **USDC**). Make sure you have sufficient balance of the initial token in your wallet.

    <figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
4. **Define the Amount and Review Slippage Tolerance**: Enter the amount you want to exchange and review the slippage tolerance (by clicking on the gear), which is the acceptable price variation during the transaction. This is especially important in volatile markets, as it protects the user from receiving less than expected if the price changes.
5.  **Confirm the Swap**: Review the exchange details, including gas fees, and confirm the transaction in your wallet. Once confirmed, the Uniswap smart contract performs the token exchange using the liquidity pool.

    <figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
6. **Receive the Tokens in your Wallet**: Once the transaction is processed, you will receive the tokens directly in your wallet. You can verify the transaction on Etherscan to ensure it has been completed correctly.
