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

# Creating ERC20 with Openzeppelin Wizard

Creating an ERC20 token from scratch can be a bit tricky, especially if you're new to Solidity. But thanks to tools like OpenZeppelin Wizard, you can now generate ERC20 contracts with just a few clicks, without needing to write a single line of code.

### What is OpenZeppelin Wizard?

OpenZeppelin Wizard is an online visual tool that allows you to create smart contracts quickly and easily, selecting the features you want to include. With this tool you can configure everything needed for your ERC20 contract, from the token name and symbol to additional functions like minting, burning, or snapshots, without worrying about technical details.

### Creating your ERC20 with OpenZeppelin Wizard: Step by Step

Let's see how to create an ERC20 token using this amazing tool.

**1. Access OpenZeppelin Wizard**

The first thing you need to do is go to the OpenZeppelin Wizard page. Here you'll see a friendly interface that allows you to configure various types of contracts, including ERC20, ERC721 (NFTs) and more.

{% embed url="https://wizard.openzeppelin.com/" %}

**2. Configure the ERC20 Token**

* **Select the contract type:** In the ERC20 section, you can configure the following parameters:
  * **Token Name:** Choose the name your token will have, I'll call it "Genesis".
  * **Token Symbol:** This is the symbol that will represent your token, in my case "GNS". It's like FCB for FC Barcelona, or COL for Colombia.
  * **Premint:** The number of tokens that will be created when deploying the contract. For example, you can set it to 1,000,000.
* **Additional features:**
  * **Mintable:** Allows creating more tokens after the initial deployment. Ideal if you want to have the ability to increase the number of tokens in circulation.
  * **Burnable:** Users can burn (destroy) their own tokens, reducing the total amount in circulation.
  * **Pausable:** Gives you the option to pause transfer functions in emergency cases.
  * **Ownable:** Ideal for controlling access to specific functions, defining a contract owner who can transfer ownership to another user.

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

**3. Generate the Code**

Once you've configured all the options according to your needs, click on the "Open in Remix" button or simply copy and paste it.&#x20;

**4. Deploy the Contract in Remix**

If you've chosen to open the code in Remix, follow these steps to deploy your token:

1. **Connect to Remix:** Go to [Remix IDE](https://remix.ethereum.org/).
2. **Load the Code:** Copy and paste the code generated in OpenZeppelin Wizard into a new file within Remix.
3. **Compile:** Click on the "compile" icon to make sure the code has no errors.
4. **Deploy:** Select "Deploy" and choose the Avalanche Testnet (Fuji) network. Depending on the additional features you add, it will ask you to enter values as parameters, in my case, when adding Ownable, it will ask for the address that will own the contract.
5. **Verify:** Use the verification plugin to verify your ERC20 contract.
6. **Wallet:** When opening your Core wallet, you'll see your tokens automatically reflected.

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

**5. Interact with your Token**

Congratulations! Now you have your own ERC20 token deployed. You can interact with it directly from Remix or use Core to send, receive and view your tokens.

Try sending me some of your tokens! Go to Remix and go to the deployed contracts section, now, execute the `transfer` function, passing as parameter the recipient's address (0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702), and the amount of tokens you want to send, remember to take into account the number of decimals you have defined, if you're going to send 50 tokens, you should enter 50 \* 10^`decimals`. In my case I left the default value (18), so I should enter 50 \* 10^18.

```
// Address
0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702
// Amount to transfer (50 * 10^18)
50000000000000000000
```

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

### Advantages of Using OpenZeppelin Wizard

1. **Simplicity:** You don't need to be a Solidity expert to create a functional and secure token. OpenZeppelin Wizard takes care of the hard part.
2. **Security:** The generated contracts follow OpenZeppelin standards, ensuring they are secure and aligned with industry best practices.
3. **Customization:** You can choose exactly what features you want in your token, ensuring it fits your project's needs without adding unnecessary complexity.
