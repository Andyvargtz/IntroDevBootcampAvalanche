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

# Compile a Contract

We already have our contract, now what we need to do is compile it. This process converts the high-level code you wrote in Solidity into a language that the blockchain can understand and execute.

When you write a smart contract in **Solidity**, you do it in a developer-friendly language, but blockchains don't directly understand this code. This is where **compilation** comes in, converting the Solidity code into **bytecode**, which is the format that the Ethereum Virtual Machine (EVM) can execute.

Compilation also generates something called **ABI** (Application Binary Interface), which is a format that describes how to interact with the contract, what functions it has, what inputs it needs, and what type of data it returns. Without the ABI, decentralized applications wouldn't know how to communicate with your contract.

## Basic Compilation Steps

To compile our contract, the first thing we'll do is go to the "Solidity compiler" section in the left panel:

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Make sure the compiler version falls within the range you defined in the pragma, in our case it should be from 0.8.20 onwards:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### Compiler Options

Then you'll see there are 3 checkboxes, I'll explain what each one does:

* **Include nightly builds:** Allows you to use the most recent and unstable versions of the Solidity compiler, known as "nightly builds". These can be unstable and contain unidentified errors, so it's recommended to use them only if you need to test something specific that hasn't been officially released yet.
* **Auto compile:** Remix will automatically compile your contract every time you make a change to the code. This option is useful because it saves you the effort of manually compiling each time you make a change, allowing you to see in real-time if there are errors or warnings in the code as you write it.
* **Hide warnings:** Allows you to hide warnings generated during compilation. Although warnings are not critical errors, they can indicate potential problems or bad practices in the code. If you choose to hide them, you won't see these messages in the console, which could make you miss important warnings that might prevent future errors.

### Manual Compilation

To compile your contract manually, you just need to click on the big blue button that says **Compile** plus the contract name. Or you can also do it by pressing **Ctrl + S**.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

If there are no errors, a green checkmark will appear on the left panel icon, with the message "Compilation successful".

### Additional Compilation Options

Below you'll see another gray button that says "Compile and Run script", which is generally not used much. Its function is to compile and immediately execute scripts (usually in Javascript or Typescript) in the Remix environment. I would recommend using tools like Hardhat or Foundry instead of this.

One section that often confuses many is the one below, "CONTRACT". A `.sol` file can have multiple contracts, and in turn, those contracts can be importing other contracts. In this section, you can specify which of all the contracts is the one you want to compile. In our case, we only have one contract, so we don't need to worry about this for now.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

## Advanced Compiler Settings

Sometimes, due to different circumstances, we'll need to use advanced configurations.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

### Configuration Options

* **Configuration Method:** Choose between configuring the compiler through the interface or via a .JSON file. By default, it's through the interface.
* **Language:** Define the language for writing smart contracts. You have two options: Solidity or YUL (an intermediate representation used by Solidity). In most cases, **Solidity** is what you need.
* **EVM Version:** The dropdown list allows you to compile code for a specific **Ethereum version**. Generally, it's left as default.
* **Enable Optimization:** Allows you to enable **optimization** during compilation. When activated, the compiler attempts to reduce the contract's bytecode size or gas usage (transaction costs). You can adjust the number of iterations to determine how much you want to optimize the contract, although the default value (200) is usually sufficient in most cases.

### Compilation Tools

Remix also offers a series of tools that we can use when compiling our contract:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

* **Run Remix Analysis:** Analyzes your contract looking for errors and security and optimization warnings. However, it's a relatively new tool, so it still has many bugs and tends to be confusing.
* **Run SolidityScan:** Performs a security analysis to detect specific vulnerabilities in the contract.
* **Publish on IPFS:** Publishes your contract on a decentralized file-sharing network (IPFS), making the code publicly accessible.
* **Publish on Swarm:** Similar to IPFS, it allows you to store your contract on a decentralized network specific to the Ethereum ecosystem.
* **Compilation Details:** Provides technical details such as bytecode, ABI, estimated gas usage, and other important information generated during compilation.

### Accessing Compilation Results

Finally, at the bottom, we have the option to copy the **ABI** and **Bytecode**.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

## Understanding Compilation Results

When you successfully compile a contract, you'll get two important pieces of information:

1. **ABI (Application Binary Interface):** This is a JSON file that describes how to interact with your contract. It includes:
   - Function names and their parameters
   - Return types
   - Event definitions
   - Contract state variables

2. **Bytecode:** This is the compiled version of your contract that will be deployed to the blockchain. It's a hexadecimal string that represents the machine code the EVM will execute.

### Common Compilation Errors

Here are some common errors you might encounter during compilation:

* **Version Mismatch:** When the compiler version doesn't match the pragma directive in your contract.
* **Syntax Errors:** Missing semicolons, incorrect function declarations, etc.
* **Type Errors:** Trying to assign incompatible types or using undefined variables.
* **Import Errors:** When the compiler can't find imported files or contracts.

### Best Practices

1. **Always check compiler warnings:** Even if your contract compiles successfully, warnings can indicate potential issues.
2. **Use the latest stable compiler version:** Unless you have a specific reason not to.
3. **Enable optimization for production:** This can significantly reduce gas costs.
4. **Keep your imports organized:** Use clear and consistent import paths.
5. **Test thoroughly after compilation:** Just because it compiles doesn't mean it works as intended.

Remember that compilation is just the first step. After successful compilation, you'll need to deploy your contract to test it properly.
