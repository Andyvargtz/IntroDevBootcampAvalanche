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

# Creating ERC721 with Openzeppelin Wizard

Creating an **ERC721** token from scratch can be challenging, especially if you're new to Solidity. However, thanks to tools like **OpenZeppelin Wizard**, you can generate ERC721 contracts easily and quickly, without writing code from scratch.

### What is OpenZeppelin Wizard?

**OpenZeppelin Wizard** is an online visual tool that facilitates the creation of smart contracts, allowing you to choose the specific features you want to include in your contract. With this tool, you can easily configure all aspects of your ERC721 contract, such as name, symbol, and additional features like safe minting and burn capability, without worrying about technical details.

### Creating your ERC721 with OpenZeppelin Wizard: Step by Step

Let's see how to create an ERC721 token using this powerful tool.

**1. Access OpenZeppelin Wizard**

To begin, visit the **OpenZeppelin Wizard** page. You'll find a user-friendly interface where you can configure various types of contracts, including ERC20, ERC721 (NFTs), and more.

{% embed url="https://wizard.openzeppelin.com/#erc721" %}

**2. Configure the ERC721 Token**

* In the **ERC721** section of the Wizard, you can configure the following parameters:
  * **Token Name**: Set the name of your NFT collection. For example, you could call it "Membership".
  * **Token Symbol**: This is the abbreviated symbol that will represent your collection, such as "MEM" for "Membership".
  * **Base URI**: Configure the base URI that will be used for each NFT's metadata. This allows each token to have a specific URI by concatenating the `tokenId` with the base URI you define.
* **Additional Features:**
  * **Mintable**: Allows creating (minting) new NFTs after initial deployment. Ideal if you plan to have a collection that grows over time.
  * **Auto Increment IDs**: Automates the assignment of incremental IDs for each new minted token, eliminating the need to manually set the `tokenId` each time a new NFT is created.
  * **Burnable**: Gives users the possibility to burn (destroy) their NFTs, permanently removing them from the collection.
  * **Pausable**: Gives you the option to pause transfer functions in emergency cases.
  * **Ownable**: Defines a contract owner with exclusive permissions, which is useful for controlling collection administration.
  * **Enumerable**: Allows tracking all issued tokens. This is useful if you want to list all NFTs in the collection or verify how many have been minted.
  * **URI Storage**: Provides the possibility to store specific URIs for each token, instead of relying on a base URI. This allows each token to have its own personalized link to unique metadata.

**3. Generate the Code**

After configuring all options to your liking, click the **"Open in Remix"** button to open the contract in Remix IDE, or simply copy the generated code and paste it into a file within Remix.

**4. Deploy the Contract in Remix**

If you've chosen to open the code in Remix, follow these steps to deploy your NFT collection:

* **Connect to Remix**: Open Remix IDE.
* **Load the Code**: Copy and paste the code generated in OpenZeppelin Wizard into a new file within Remix.
* **Compile**: Click the "compile" icon to ensure the code has no errors.
* **Deploy**: Select "Deploy" and choose the Avalanche Testnet (Fuji) network or your preferred network. Depending on the additional features you've included, such as `Ownable`, you may need to provide an owner address.
* **Verify**: Use the verification plugin in Remix to verify your ERC721 contract.

**5. Interact with your NFT Token**

Congratulations! You now have your own NFT collection on the blockchain. You can interact with your ERC721 contract directly from Remix or, if you have an NFT-compatible wallet, you'll be able to see your tokens.

### Example of NFT Minting

From Remix, you can mint a new NFT by executing the `mint` function, passing as parameters the recipient's address and the unique `tokenId`. With **Auto Increment IDs**, the `tokenId` will be assigned automatically.

```
// Address
0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702
```

In the case of an ERC721 token, it's not necessary to handle decimals as with ERC20, since each token is unique and indivisible.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
