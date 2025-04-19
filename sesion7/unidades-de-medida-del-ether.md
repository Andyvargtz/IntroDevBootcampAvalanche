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

# Ether Units of Measurement

In the EVM, not everything is measured in Ether as such. There are different units to represent amounts of this cryptocurrency, similar to how we use grams, kilograms, and tons to measure weight. Understanding these units is key to not getting lost in the vastness of zeros and decimals that sometimes accompany network transactions. Let's get to know them!

### What is Ether and why does it have so many units?

Ether (ETH) is the native cryptocurrency of the Ethereum network and is used to pay gas fees, deploy smart contracts, and much more. But since handling very small or very large amounts of Ether can become cumbersome, different units were created to facilitate its use. Each of these units represents a specific fraction of Ether, similar to how a dollar has cents.

{% hint style="info" %}
Even though we're working on a different network than Ethereum, like Avalanche, Polygon, or Binance Smart Chain, which have their own native token, the term Ether or ETH is still used to refer to the units of measurement.
{% endhint %}

### Main Ether Units of Measurement

1.  **Wei**: It's the smallest unit of Ether, like the atom of the blockchain universe. Think of `wei` as the "penny" of Ether, but instead of being a hundredth part, it's an eighteenth part! One Ether has exactly `1,000,000,000,000,000,000` (one quintillion) Wei. Basically, if you see a huge number with many zeros, you're probably looking at Wei.

    **Example**: 1 ETH = 1,000,000,000,000,000,000 Wei
2.  **Gwei**: Also known as "shannon", it's the most common unit when talking about gas fees in Ethereum. 1 Gwei is equal to `1,000,000,000` Wei (one billion). If you've ever seen a transaction fee in Gwei, it's because it's the most practical way to express fees without using so many zeros.

    **Example**: 1 Gwei = 1,000,000,000 Wei
3.  **Ether**: It's the main and most well-known unit, used to represent balances and larger transactions. If someone tells you they have 5 ETH, that's 5 complete Ethers, without any subdivision.

    **Example**: 1 Ether = 1,000,000,000,000,000,000 Wei

### Comparative Table of Units

| **Unit**    | **Symbol** | **Value in Wei**          | **Description**       |
| ----------- | ---------- | ------------------------- | --------------------- |
| Wei         | wei        | 1                         | Smallest unit         |
| Kwei        | babbage    | 1,000                     | 1,000 Wei             |
| Mwei        | lovelace   | 1,000,000                 | 1 million Wei         |
| Gwei        | shannon    | 1,000,000,000             | 1 billion Wei         |
| Microether  | szabo      | 1,000,000,000,000         | 1 trillion Wei        |
| Milliether  | finney     | 1,000,000,000,000,000     | 1 quadrillion Wei     |
| Ether       | eth        | 1,000,000,000,000,000,000 | 1 quintillion Wei     |

### Why so many units?

The different units are useful for representing different amounts of Ether without dealing with heaps of zeros. Imagine having to express a transaction of 0.000000001 ETH in Wei: it would be a huge and complicated number to handle. Instead, we say 1 Gwei, and that's it. The units also help avoid errors, as it's easy to get confused when dealing with numbers like `1000000000000000000` (1 Ether in Wei).

### When to use each unit?

1. **Wei**: Ideal for precise and small calculations, like dividing Ether into extremely small parts.
2. **Gwei**: The most used option for gas fees. If you see fees like 30 Gwei, it means each unit of gas costs 30 Gwei.
3. **Ether**: Used to represent complete amounts of the currency, like account balances or larger transactions.
