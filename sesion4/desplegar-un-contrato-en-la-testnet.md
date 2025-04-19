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

# Deploy a Contract to the Testnet

You already have your smart contract written and compiled. Now comes the exciting part, **deploying it to the blockchain**. When we talk about "deploying" a contract, we refer to the process of uploading your contract to the blockchain so that it is publicly available and anyone can interact with it.

You cannot change the code once the contract is deployed, so it is essential to make sure everything works correctly before taking this step.

Additionally, each contract deployment requires a **transaction** on the blockchain, which means you will need to pay **gas fees** (transaction fees) with the cryptocurrency of the network you are using, such as **ETH** on Ethereum or **AVAX** on Avalanche's C-Chain.

### How to deploy a contract in Remix

Here are the steps to deploy a contract using **Remix**:

1. **Select the "Deploy & Run Transactions" tab**: In the left sidebar of Remix, click on the tab icon that says **Deploy & Run Transactions**. This section will allow you to configure how and where you want to deploy your contract.

    <figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>
2. **Have your wallet ready**: If you plan to deploy your contract on a real network (either a **Testnet** or the **mainnet**), you need to connect a wallet, in this case **Core**. Make sure your wallet is configured and ready, and that it is connected to the network where you want to deploy your contract, in this case the Avalanche testnet.

    <figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>
3. **Choose the environment**: Remix allows you to choose between different networks to deploy your contract. The most common options are:

    * **Remix VM**: It's a local simulation. It's only used for testing within Remix and doesn't involve costs or deploy the contract to a real blockchain.
    * **WalletConnect**: This option is used when you're connecting your wallet, like **Core**, to deploy on **Avalanche**.

    <figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

    You might get a message saying that the app doesn't support the selected network, but this is an error, just click the "X" in the top right corner.

    <figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>
4. **Select the contract**: In the same **Deploy & Run Transactions** section, you'll see a menu where you can choose which of your contracts you want to deploy (in case you have more than one in your project). In our case, we only have one.
5. **Deploy the contract**: Once you've selected your network and the contract, you just need to click the orange button that says **"Deploy"**. This will generate a transaction on the blockchain. If you're connected to Avalanche, you'll see that your wallet will ask you to confirm the transaction and will show you the **gas fees** you need to pay.

    <figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>
6. **Verify the deployment**: When the transaction is confirmed, your contract will be deployed on the blockchain. In Remix, you'll see a new section that will allow you to interact with the contract directly. You'll also receive the **address** of the contract, which is essentially its "location" on the blockchain. With that address, anyone can interact with your contract.

    <figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

