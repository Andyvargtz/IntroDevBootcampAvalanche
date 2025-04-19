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

# Verify a Contract

Once you have deployed your smart contract to the blockchain, the next step is to **verify it**. Verifying a contract is a process that allows anyone to see the source code of your contract on the blockchain, adding an important layer of **transparency**.

### Steps to verify a contract

Verifying a contract is easier than it seems. Below I explain how to do it step by step:

1.  **Copy the contract address:** Simply copy the address of the contract you deployed in Remix.

    <figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>
2.  **Access the block explorer**: Go to the block explorer of the network where you deployed your contract. If it's on Avalanche, use [**SnowScan**](https://snowscan.xyz/)**.** Then click on **Sign In** in the top right corner.

    <figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>
3.  **Create your account:** If you don't have an account yet, you can create one by clicking on **Sign Up.**

    <figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>
4.  **Go to the "API Keys" section**: Once in your account, look for the option that says "API Keys" in the left panel.

    <figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>
5. **Add an API**: Now, click on the blue "Add" button and assign it a name. Copy the API Key Token, it will be useful for easily verifying smart contracts on Avalanche.
6.  **Enter the Plugin Manager**: Next, you should look for the "CONTRACT VERIFICATION - ETHERSCAN" extension in Remix's Plugin Manager.

    <figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>
7.  **Verify**: Once activated, you can enter the plugin through the left panel, the first thing it will ask for is the API Key Token, you just need to paste it. Now, it will ask you to select the contract and enter the Contract Address you copied in step 1. Then click the blue "Verify" button.

    <figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>
8.  **Confirm the verification**: If the verification process was successful, your contract code should appear in the verifier.

    * Enter the Avalanche block explorer, in this case, since we deployed on Fuji, we must enter the testnet version of the explorer. You can [enter here](https://testnet.snowtrace.io/).
    * Enter the contract address in the search bar and press _enter_.
    * Click on the "contract" tab.

    <figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

Your contract is verified! Now you can see that next to the **Code** tab, there are two more tabs, Read Contract and Write Contract, which will help us interact with the contract.
