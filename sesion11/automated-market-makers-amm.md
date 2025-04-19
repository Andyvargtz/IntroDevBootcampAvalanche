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

# Automated Market Makers (AMM)

To understand how we arrived at **Automated Market Makers (AMM)** and **liquidity pools** in decentralized finance, it's helpful to start with a parallel we all know, traditional stock and currency markets, where supply and demand determine the price of each asset.

### A Brief History

In an isolated and hidden place among the mountains, there was a small village called **Hills Village**. This village was famous because its inhabitants, the **Hydros** and the **Orios**, used different coins, the Hydros used **hydrocoins** and the Orios, **oriocoins**. Although both lived in peace, the coins were not compatible and exchange between the two groups was a challenge that complicated village life. For years, the villagers relied on an informal barter system, where they had to find someone who needed exactly what they offered at the right time.

**The Arrival of the Market Bridge**

One day, a traveling merchant named **Arthur** arrived in the village and noticed the villagers' difficulties in exchanging hydrocoins and oriocoins. Determined to help, Arthur proposed building a **market bridge** between both parts of the village, where villagers could meet and trade easily. The bridge would allow villagers to make exchanges without having to find an exact counterpart, using an order book to record their offers and demands.

However, Arthur soon realized that this system had its problems: finding matches in the order book wasn't easy, and long lines and delays made the villagers impatient. The barter system was slow and, although better than before, the village still faced many limitations.

**The Innovation of the Liquidity Pool**

Inspired by the problem, Arthur had a revolutionary idea, what if he created a "pool" where villagers could **deposit their hydrocoins and oriocoins** so that anyone could make exchanges without needing exact matches? This would be the **Liquidity Pool**. Arthur explained his idea to the villagers, they could leave their coins in the pool and in return receive a percentage of the fees generated each time someone used the pool to make an exchange.

This system turned out to be a success. The villagers began depositing their coins in the pool, and whenever someone needed to exchange hydrocoins for oriocoins, they simply took what they needed, paying a small fee that was distributed among the liquidity providers. Now, any villager could change their coins without waiting for a perfect match, and the market bridge transformed into a dynamic and efficient place.

**The Scarcity Problem**

Everything seemed to work well until one day a problem arose: **the Hydros** started crossing more into the Orios' territory to exchange, and the hydrocoin pool began to deplete quickly. The villagers realized that if one coin became scarce, exchanges became very expensive and the balance was broken. Arthur understood that he needed a mechanism that would keep the pool automatically balanced without depleting one of the coins.

It was then that he came up with an approach based on a **constant product** instead of a constant sum. In this system, known as **x * y = k**, the amount of hydrocoins and oriocoins was always multiplied to maintain balance. This meant that as one coin became scarce, its price increased, incentivizing villagers to make exchanges in the opposite direction and maintaining the balance on both sides of the pool.

**The Emergence of Liquidity Providers**

With the success of Arthur's system, more villagers wanted to deposit their coins in the pool and earn a share of the fees. Arthur began issuing **participation certificates** to each liquidity provider, so that each one had a proportion of the pool according to their contribution. Now, villagers not only exchanged coins easily, but could also earn passive income from their deposits.

However, some villagers began to notice that when the price of a coin varied too quickly, their participation in the pool was affected by something called **impermanent loss**. Although this phenomenon could cause some disadvantage, most villagers considered that the benefits of the pool outweighed the risks, and continued using the system to facilitate life in the village.

**The Legacy of Arthur's Bridge**

Thanks to Arthur's creativity, the market bridge transformed the economy of Hills Village. The AMM system and liquidity pools boosted the trade of hydrocoins and oriocoins, and over time, villagers from other regions began to arrive to see this wonder. Arthur had created not only an efficient exchange system, but a model for the future of decentralized markets.

### What is an Automated Market Maker (AMM)?

**Automated Market Makers (AMM)** are smart contracts that allow the exchange of assets in a market without depending on a traditional order book, like the one Arthur had initially created in the village. Instead of looking for a direct match between buyers and sellers, AMMs use **liquidity pools** where users deposit token pairs. This system ensures that there is always liquidity available and allows any user to perform exchanges smoothly and automatically.

**The Constant Product Formula: x * y = k**

To maintain the balance between two coins in the liquidity pool, AMMs apply the formula **x * y = k**, where "x" and "y" represent the amount of each token in the pool and "k" is a constant. This formula ensures that as the amount of one coin decreases, its price rises, incentivizing trade in the opposite direction and preventing it from being completely depleted, similar to how Arthur adjusted prices in the village's liquidity pool.

**Incentives for Liquidity Providers (LP)**

In an AMM, users can become **liquidity providers (LP)**, depositing token pairs in the pool in exchange for a share of the fees generated by the exchange of those tokens. Just as in the story the villagers received a reward for their deposits, in AMMs LPs obtain passive income, which motivates participation and ensures the constant availability of assets in the pool.

### AVAX/USDC Exchange Example

To understand how AMMs work in practice, let's take the example of a **liquidity pool between AVAX and USDC**. Imagine we're using an AMM on a DEX like **Pangolin** (a decentralized exchange operating on the Avalanche network), where users can exchange AVAX for USDC and vice versa.

Suppose someone wants to exchange 1 AVAX for USDC. In this case, the DEX consults the liquidity pool between AVAX and USDC, which already has an amount of each token deposited, for example, 1,000 AVAX and 10,000 USDC. The AMM formula ensures that the ratio of both tokens remains balanced, in this case under the equation _**x * y = k**_, where _**x**_ is the amount of AVAX in the pool, _**y**_ is the amount of USDC, and _**k**_ is a fixed constant. This means that when adding or removing AVAX or USDC, the price of each changes to maintain balance.

* **Initial State**:
  * The pool contains 1,000 AVAX and 10,000 USDC, with a constant _**k = 1,000,000**_.
  * This means that the price of 1 AVAX is 10 USDC (because the current pool balance is 1,000 AVAX per 10,000 USDC).
* **Exchange**:
  * A user deposits 1 AVAX in the pool and withdraws an amount of USDC.
  * Since there are now 1,001 AVAX in the pool, the AMM adjusts the amount of USDC available to maintain the constant _**k**_.
  * The AMM withdraws an amount of USDC, say 9.90 USDC, which is less than 10 due to the fluctuation caused by the change in the ratio of both tokens in the pool.
* **New Balance**:
  * After the exchange, the pool has 1,001 AVAX and 9,990.1 USDC.
  * This means that the price of AVAX in terms of USDC has increased slightly, incentivizing other users to exchange in the opposite direction (USDC to AVAX) to balance the pool.
