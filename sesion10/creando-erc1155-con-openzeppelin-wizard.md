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

# Creating ERC1155 with Openzeppelin Wizard

Creating a contract for multiple types of tokens (fungible and non-fungible) can be complicated, but thanks to **OpenZeppelin Wizard**, you can configure and deploy your ERC1155 contract quickly and easily, without needing to write code from scratch.

### Creating your ERC1155 with OpenZeppelin Wizard: Step by Step

Below, we show you how to create an ERC1155 contract using this powerful tool.

**1. Access OpenZeppelin Wizard**

To begin, visit OpenZeppelin Wizard. You'll find an easy-to-use interface where you can configure various types of contracts, including ERC20, ERC721, and ERC1155.

**2. Configure the ERC1155 Token**

In the **ERC1155** section of the Wizard, configure the following parameters:

* **Name**: Specify the name of your contract, for example, "MyToken".
*   **URI**: Define the base URI for all token types. The URI must contain `{id}` where it will be automatically replaced with the token's `id`. An example would be:

    ```arduino
    ipfs://QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json
    ```

    This allows each token type to point to its specific metadata based on its `id`.

**Additional Features:**

* **Mintable**: Allows the creation of new tokens after initial deployment, which is ideal if you plan to add different items or assets to your contract in the future.
* **Burnable**: Gives users the option to burn (destroy) their own tokens, which reduces the total supply of those tokens.
* **Supply Tracking**: Enables supply tracking, allowing you to query the total amount of each token type in circulation.
* **Pausable**: Provides the ability to pause transfers in emergency cases, adding an extra layer of security.
* **Updatable URI**: Allows modifying the base URI after deployment, useful if you need to update the location of metadata.

**3. Generate the Code**

Once you've configured all options according to your needs, click the **"Open in Remix"** button to open the code in Remix IDE, or copy the generated code and paste it into a file within Remix.

**4. Deploy the Contract in Remix**

If you chose to open the code in Remix, follow these steps to deploy your ERC1155 contract:

* **Connect to Remix**: Open Remix IDE.
* **Load the Code**: Copy and paste the code generated in OpenZeppelin Wizard into a new file in Remix.
* **Compile**: Click the "compile" icon to ensure the code has no errors.
* **Deploy**: Select "Deploy" and choose the Avalanche Testnet (Fuji) network or your preferred network. Depending on the selected configurations, you may need to assign an owner or role if you've enabled `Access Control`.
* **Verify**: Use the verification plugin in Remix to verify the ERC1155 contract, facilitating transparency and code validation.

**5. Interact with your Tokens**

Congratulations! You now have a deployed ERC1155 contract that allows the creation of multiple types of tokens. You can interact with it from Remix, mint different types of tokens, burn them, or manage access roles.

### Example of Token Minting

From Remix, you can mint a new token using the `mint` function, passing as parameters the recipient's address, the token's `id`, and the desired amount.

* **Address**: 0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702
* **Token ID**: 1 (for a specific type of token).
* **Amount**: 100 (in the case of a fungible token, you can set any amount).

To create multiple types of tokens in a single transaction, use the `mintBatch` function, which is ideal if you want to add several items or assets at once.
