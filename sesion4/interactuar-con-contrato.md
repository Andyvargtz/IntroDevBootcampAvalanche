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

# Interact with Contract

Once your contract has been deployed and verified, you can now **interact with it**. Interacting with a smart contract means using its functions, either to read information or to perform actions on the blockchain. There are two main ways to interact with a contract, directly from **Remix** or using a **block explorer** like **Snowtrace**.

### Interact with a contract from Remix

Remix is not only useful for developing and deploying contracts, but it also allows you to interact with them once they are deployed. Here's how to do it:

1. **Deployment section**: If you already have your contract deployed, go to the **"Deploy & Run Transactions"** tab in Remix.
2.  **Select the deployed contract**: In the **Deployed Contracts** section of Remix, you'll see a list of contracts you've deployed. Each contract will have its own expandable section where you can see the available functions.

    <figure><img src="../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>
3.  **Execute functions**: Simply click on the functions you want to execute. If the function is read-only (like `leerMensaje`), it will execute without cost. But if the function modifies the blockchain state (for example, if you send funds or change a variable, as in the case of `enviarMensaje`), you'll need to pay **gas** to process the transaction. In this case, Remix will ask you to confirm the transaction. In our case, we'll first execute `enviarMensaje`, entering as a parameter the text you want. Once the transaction is confirmed, execute `leerMensaje`, and you'll see that the variable stored the value correctly.

    <figure><img src="../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
If you get any error when executing the `leerMensaje` function, you might be having compatibility issues with the EVM version. To solve it, go to the advanced compiler settings and change the EVM VERSION to **shanghai**. Then, redeploy the contract.
{% endhint %}

### Interact with a contract from a block explorer

If you prefer to interact with your contract directly from a **block explorer** like **Snowtrace**, it's also possible and very useful, especially if your contract is already on a public network and you want other users to be able to interact with it without having to use Remix.

1. **Access the block explorer**: Go to the [**Snowtrace** ](https://testnet.snowtrace.io/)block explorer in the test version (Fuji).
2.  **Search for the contract address**: Use the contract address to search for it in the block explorer. Once you find it, you'll see a tab called **"Contract"** where you can see its information.

    <figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>
3.  **Go to "Write Contract" or "Read Contract"**: Depending on what you want to do, you can go to the **"Read Contract"** tab to see stored data (for example, balances or states), or to **"Write Contract"** if you want to execute a function that modifies the contract state (like transferring tokens, sending funds, or interacting with a dApp).

    \[**Image**: Etherscan screen showing the "Read Contract" and "Write Contract" tabs.]
4. **Connect your wallet**: If you want to execute a function that involves changes to the blockchain, you'll need to connect your Core wallet to sign and send the transaction. This is done directly from the block explorer.
5.  **Execute functions**: Just like in Remix, you can execute the available functions in the contract. Just remember that functions that modify the blockchain will require paying gas fees.

    <figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>
