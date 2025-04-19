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

# Dynamic NFTs

**Dynamic NFTs** represent a significant evolution in non-fungible token technology, as they allow the NFT's metadata to change in response to certain events or conditions. In the context of **Real World Assets (RWA)**, dynamic NFTs present a unique opportunity to represent assets whose value, properties, or state can vary over time, providing a more accurate and real-time representation of real-world assets.

### **What is a Dynamic NFT?**

A **dynamic NFT** is a non-fungible token whose information or metadata can be automatically updated based on changes in the real world or on the blockchain. Unlike traditional NFTs, which have fixed characteristics, dynamic NFTs can adapt to specific conditions through the integration of **oracles**, **smart contracts**, and **external events**.

Example: Imagine you own an NFT representing a real estate property. With a dynamic NFT, the property's market value, its condition, or any renovations made to it can be automatically reflected in the NFT as these changes occur.

### **Use Cases of Dynamic NFTs in RWA**

1. **Real Estate Properties**
   * Dynamic NFTs can represent properties whose market values fluctuate over time. Each change in value, such as a renovation or an update in appraisal, can be automatically reflected in the NFT.
   * **Practical example**: An NFT representing a building can update its value quarterly based on the local market price, also showing information about the property's condition, such as if it needs repairs or has been recently renovated.
2. **Automobiles and Durable Goods**
   * For assets like automobiles, a dynamic NFT can record mileage, maintenance history, and wear, allowing potential buyers to evaluate the current state of the vehicle without relying on intermediaries.
   * **Practical example**: An NFT of a car that changes its value and conditions every time a major repair is made or after a technical inspection, allowing buyers to have an updated history at all times.
3. **Financial Instruments and Securities**
   * Dynamic NFTs can represent bonds, stocks, and other financial instruments whose values and conditions change in real-time.
   * **Practical example**: A tokenized bond as an NFT can automatically reflect interest payments made and changes in the interest rate, providing investors with an updated view of their investment.
4. **Commodities and Natural Resources**
   * Assets like gold, oil, and other commodities can be tokenized into dynamic NFTs that reflect the current market value and variations in their quantity or quality.
   * **Practical example**: An NFT representing a gold mine could update the value of remaining reserves and reflect the current price of gold, providing a real-time representation of available resources.

### **Implementation of a Dynamic NFT: RealEstateNFT Contract**

Below is a contract representing a **dynamic NFT** for a real-world asset, such as a real estate property, whose value is automatically updated based on data provided by an oracle (simulated here). This example uses **OpenZeppelin** for basic NFT functions and **Chainlink** as a price oracle:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract RealEstateNFT is ERC721URIStorage, Ownable {
    uint256 public tokenId;
    AggregatorV3Interface internal priceFeed;

    // Mapping to store current asset values
    mapping(uint256 => uint256) public assetValues;

    // Event for NFT value change
    event AssetValueUpdated(uint256 tokenId, uint256 newValue);

    constructor(address _priceFeed) ERC721("RealEstateNFT", "REALE") {
        priceFeed = AggregatorV3Interface(_priceFeed);
    }

    // Function to mint a new NFT and set an initial value
    function mintNFT(address recipient, string memory tokenURI, uint256 initialValue) public onlyOwner {
        _mint(recipient, tokenId);
        _setTokenURI(tokenId, tokenURI);
        assetValues[tokenId] = initialValue;
        tokenId++;
    }

    // Function to update asset value from an external oracle
    function updateAssetValue(uint256 _tokenId) public onlyOwner {
        require(_exists(_tokenId), "Token does not exist.");
        
        // Get current price from oracle (simulated)
        (, int price, , ,) = priceFeed.latestRoundData();
        uint256 newValue = uint256(price);

        // Update asset value
        assetValues[_tokenId] = newValue;
        
        emit AssetValueUpdated(_tokenId, newValue);
    }

    // Get current asset value
    function getAssetValue(uint256 _tokenId) public view returns (uint256) {
        require(_exists(_tokenId), "Token does not exist.");
        return assetValues[_tokenId];
    }
}
```

1. **Imports**: This contract uses OpenZeppelin's `ERC721URIStorage` extension to handle token URIs and `Ownable` to control owner-only functions.
2. **Price Oracle**: This contract assumes the existence of an oracle (e.g., Chainlink) that provides the asset's value. Here, the oracle is initialized in the constructor.
3. **NFT Minting**: The `mintNFT` function allows the owner to create a new NFT to represent a real estate asset. Each token is assigned a URI and an initial value.
4. **Value Update**: The `updateAssetValue` function obtains the most recent asset value from the oracle and updates the token's value in the contract. This update can only be performed by the contract owner.
5. **Value Query**: The `getAssetValue` function allows any user to check the current value of the asset represented by the NFT.

### **Benefits of Dynamic NFTs in RWA**

Dynamic NFTs provide **transparency and accuracy** in representing real-world assets. With this approach, investors can access a real-time view of their asset without the need for intermediaries, which improves trust and efficiency in the tokenized asset market.
