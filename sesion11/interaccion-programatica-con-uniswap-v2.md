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

# Programmatic Interaction with Uniswap V2

**Programmatic interaction with Uniswap V2** allows developers to integrate and automate operations such as token swaps, liquidity aggregation, and price queries directly from smart contracts or decentralized applications (dApps). This is possible thanks to the contracts and interfaces that Uniswap offers to interact with its liquidity pools and perform decentralized transactions.

### **Performing a Token Swap**

To perform a **token swap** in Uniswap V2, the **UniswapV2Router02** contract is used. This contract contains several functions for exchanging tokens, such as `swapExactTokensForTokens`, `swapTokensForExactTokens`, among others. Below is a basic example of how to execute a swap in Uniswap.

1.  **Configure the Router Contract**: The address of the `UniswapV2Router02` contract must be available in the script.&#x20;

    For the Ethereum mainnet, the address is: `0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D`.

    For the Sepolia network, the address is:

    `0xeE567Fe1712Faf6149d80dA1E6934E354124CfE3`.
2. **Perform an Exact Token Swap**:
   * The `swapExactTokensForTokens` function allows exchanging a specific amount of one token for another, respecting a specified minimum output.
   *   Example in Solidity:

       ```solidity
       function swapTokens(address tokenIn, address tokenOut, uint amountIn, uint amountOutMin, address to) external {
           IERC20(tokenIn).approve(address(router), amountIn);
           address;
           path[0] = tokenIn;
           path[1] = tokenOut;

           router.swapExactTokensForTokens(
               amountIn,
               amountOutMin,
               path,
               to,
               block.timestamp
           );
       }
       ```
   * **Key Parameters**:
     * `amountIn`: Amount of tokens the user wants to exchange.
     * `amountOutMin`: Minimum amount of tokens the user accepts to receive, to protect against price changes.
     * `path`: Exchange path; in this case, it contains two token addresses (input and output token).
     * `to`: Address that will receive the output tokens.
     * `block.timestamp`: Defines the temporal validity of the transaction to avoid delays.

### **Programmatic Exchange of AVAX and USDC on Uniswap**

Imagine a user wants to exchange **AVAX for USDC** using Uniswap V2. The Solidity script to perform this operation programmatically is similar to the `swapExactTokensForTokens` example, configured with AVAX as `tokenIn` and USDC as `tokenOut`. This transaction will take the specified amount of AVAX and automatically calculate the equivalent in USDC based on the pool's liquidity.

### **Adding and Removing Liquidity**

In addition to token exchange, Uniswap V2 allows adding and removing liquidity from pools, which is essential for users who want to earn transaction fees by providing liquidity.

1. **Add Liquidity**: The `addLiquidity` function allows depositing an equal amount of two tokens in a Uniswap pool, in exchange for LP tokens (Liquidity Provider tokens) that represent their share.
   *   Example in Solidity:

       ```solidity
       function addLiquidity(address tokenA, address tokenB, uint amountADesired, uint amountBDesired, address to) external {
           IERC20(tokenA).approve(address(router), amountADesired);
           IERC20(tokenB).approve(address(router), amountBDesired);

           router.addLiquidity(
               tokenA,
               tokenB,
               amountADesired,
               amountBDesired,
               0,
               0,
               to,
               block.timestamp
           );
       }
       ```
   * **Parameters**:
     * `amountADesired` and `amountBDesired`: Amount of each token to be deposited in the pool.
     * `0` in `amountAMin` and `amountBMin` ensures that no fewer tokens than desired are accepted in case of slippage.
     * `to`: Address that will receive the LP tokens.
2. **Remove Liquidity**: To withdraw tokens from the pool and recover the provided amount, `removeLiquidity` is used.
   *   Example in Solidity:

       ```solidity
       function removeLiquidity(address tokenA, address tokenB, uint liquidity, address to) external {
           IERC20(pair).approve(address(router), liquidity);

           router.removeLiquidity(
               tokenA,
               tokenB,
               liquidity,
               0,
               0,
               to,
               block.timestamp
           );
       }
       ```
   * Here, the amount of **LP tokens** is passed, and the contract returns the provided tokens, along with accumulated fee rewards.

### Complete Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "@uniswap/v2-periphery/contracts/interfaces/IUniswapV2Router02.sol";
import "@uniswap/v2-core/contracts/interfaces/IUniswapV2Factory.sol";

contract UniswapInteraction {
    IUniswapV2Router02 public router;
    address public owner;

    // Constructor to initialize the contract and define the Uniswap V2 router address
    constructor(address _router) {
        router = IUniswapV2Router02(_router);
    }

    // Function to perform an exact token swap on Uniswap
    function swapTokens(
        address tokenIn,
        address tokenOut,
        uint amountIn,
        uint amountOutMin,
        address to
    ) external {
        IERC20(tokenIn).approve(address(router), amountIn);

        address;
        path[0] = tokenIn;
        path[1] = tokenOut;

        router.swapExactTokensForTokens(
            amountIn,
            amountOutMin,
            path,
            to,
            block.timestamp
        );
    }

    // Function to add liquidity to the Uniswap pool
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint amountADesired,
        uint amountBDesired,
        address to
    ) external {
        IERC20(tokenA).approve(address(router), amountADesired);
        IERC20(tokenB).approve(address(router), amountBDesired);

        router.addLiquidity(
            tokenA,
            tokenB,
            amountADesired,
            amountBDesired,
            0,
            0,
            to,
            block.timestamp
        );
    }

    // Function to remove liquidity from the Uniswap pool
    function removeLiquidity(
        address tokenA,
        address tokenB,
        uint liquidity,
        address to
    ) external {
        address pair = IUniswapV2Factory(router.factory()).getPair(tokenA, tokenB);
        IERC20(pair).approve(address(router), liquidity);

        router.removeLiquidity(
            tokenA,
            tokenB,
            liquidity,
            0,
            0,
            to,
            block.timestamp
        );
    }
}
