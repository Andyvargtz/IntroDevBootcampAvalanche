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

# Programmatic Interaction with Uniswap V3

**Programmatic interaction with Uniswap V3** allows developers to perform swaps, create and manage liquidity pools, and adjust prices with precision thanks to the new concentrated liquidity structure. Unlike Uniswap V2, V3 introduces advanced features such as customizable price ranges and multiple fee tiers, which gives liquidity providers greater control over their investments.

### **Key Differences Between Uniswap V2 and V3**

* **Concentrated Liquidity**: Unlike V2, liquidity providers can specify price ranges in which they want to provide liquidity in V3. This allows for greater capital efficiency.
* **Fee Tiers**: V3 allows choosing between several fee tiers (0.01%, 0.05%, 0.3% and 1%) to adapt to the volatility and risk of each token pair.
* **NFTs for Liquidity**: Instead of LP tokens, each liquidity position in Uniswap V3 is represented by an NFT, which contains unique information about the price range and fee tier.

### **Performing a Token Swap**

In Uniswap V3, swaps can be performed using the `SwapRouter` contract. Here is an example of how to program a token swap from AVAX to USDC using Uniswap V3:

1.  **Swap Contract Setup**:

    * Example of a function to perform an exact swap in Uniswap V3:

    ```solidity
    function swapExactInputSingle(address tokenIn, address tokenOut, uint24 fee, uint256 amountIn, address recipient) external returns (uint256 amountOut) {
        // Approve the input token for the router
        IERC20(tokenIn).approve(address(swapRouter), amountIn);
        
        // Configure the parameters for the swap
        ISwapRouter.ExactInputSingleParams memory params =
            ISwapRouter.ExactInputSingleParams({
                tokenIn: tokenIn,
                tokenOut: tokenOut,
                fee: fee,
                recipient: recipient,
                deadline: block.timestamp,
                amountIn: amountIn,
                amountOutMinimum: 0,
                sqrtPriceLimitX96: 0
            });

        // Execute the swap
        amountOut = swapRouter.exactInputSingle(params);
    }
    ```

    * **Important Parameters**:
      * `fee`: Fee tier for the pair (for example, 3000 for 0.3%).
      * `amountIn` and `amountOutMinimum`: Input amount and minimum output to protect against price changes.
      * `sqrtPriceLimitX96`: Price limit in square root format, which in this case is set to zero to allow any price.

### **Adding and Removing Liquidity**

In Uniswap V3, when adding and removing liquidity, a price range is specified. This allows liquidity providers to optimize the use of their capital and maximize their returns.

1.  **Adding Liquidity in a Price Range**:

    * Example of a function to add liquidity:

    ```solidity
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint24 fee,
        int24 tickLower,
        int24 tickUpper,
        uint256 amountA,
        uint256 amountB,
        address recipient
    ) external returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1) {
        // Configure the parameters for adding liquidity
        INonfungiblePositionManager.MintParams memory params =
            INonfungiblePositionManager.MintParams({
                token0: tokenA,
                token1: tokenB,
                fee: fee,
                tickLower: tickLower,
                tickUpper: tickUpper,
                amount0Desired: amountA,
                amount1Desired: amountB,
                amount0Min: 0,
                amount1Min: 0,
                recipient: recipient,
                deadline: block.timestamp
            });

        // Add liquidity and receive a position NFT
        return nonfungiblePositionManager.mint(params);
    }
    ```

    * **Key Parameters**:
      * `tickLower` and `tickUpper`: Determine the price range where liquidity will be provided.
      * `amount0Min` and `amount1Min`: Minimum amounts that the user accepts to provide.
      * `recipient`: Address that receives the position NFT.
2.  **Removing Liquidity**:

    * Liquidity providers can remove their liquidity by returning the NFT of their position.

    ```solidity
    function removeLiquidity(
        uint256 tokenId,
        uint128 liquidity
    ) external returns (uint256 amount0, uint256 amount1) {
        // Parameters for removing liquidity
        INonfungiblePositionManager.DecreaseLiquidityParams memory params =
            INonfungiblePositionManager.DecreaseLiquidityParams({
                tokenId: tokenId,
                liquidity: liquidity,
                amount0Min: 0,
                amount1Min: 0,
                deadline: block.timestamp
            });

        // Remove liquidity
        return nonfungiblePositionManager.decreaseLiquidity(params);
    }
    ```



```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@uniswap/v3-periphery/contracts/interfaces/ISwapRouter.sol";
import "@uniswap/v3-periphery/contracts/interfaces/INonfungiblePositionManager.sol";
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract UniswapV3Interaction {
    ISwapRouter public swapRouter;
    INonfungiblePositionManager public nonfungiblePositionManager;

    constructor(address _swapRouter, address _positionManager) {
        swapRouter = ISwapRouter(_swapRouter);
        nonfungiblePositionManager = INonfungiblePositionManager(_positionManager);
    }

    function swapExactInputSingle(
        address tokenIn,
        address tokenOut,
        uint24 fee,
        uint256 amountIn,
        address recipient
    ) external returns (uint256 amountOut) {
        IERC20(tokenIn).approve(address(swapRouter), amountIn);

        ISwapRouter.ExactInputSingleParams memory params =
            ISwapRouter.ExactInputSingleParams({
                tokenIn: tokenIn,
                tokenOut: tokenOut,
                fee: fee,
                recipient: recipient,
                deadline: block.timestamp,
                amountIn: amountIn,
                amountOutMinimum: 0,
                sqrtPriceLimitX96: 0
            });

        amountOut = swapRouter.exactInputSingle(params);
    }
    
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint24 fee,
        int24 tickLower,
        int24 tickUpper,
        uint256 amountA,
        uint256 amountB,
        address recipient
    ) external returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1) {
        IERC20(tokenA).approve(address(nonfungiblePositionManager), amountA);
        IERC20(tokenB).approve(address(nonfungiblePositionManager), amountB);

        INonfungiblePositionManager.MintParams memory params =
            INonfungiblePositionManager.MintParams({
                token0: tokenA,
                token1: tokenB,
                fee: fee,
                tickLower: tickLower,
                tickUpper: tickUpper,
                amount0Desired: amountA,
                amount1Desired: amountB,
                amount0Min: 0,
                amount1Min: 0,
                recipient: recipient,
            deadline: block.timestamp
        });

        // Add liquidity and receive a position NFT
        return nonfungiblePositionManager.mint(params);
    }
    
    function removeLiquidity(
        uint256 tokenId,
        uint128 liquidity
    ) external returns (uint256 amount0, uint256 amount1) {
        // Parameters for removing liquidity
        INonfungiblePositionManager.DecreaseLiquidityParams memory params =
            INonfungiblePositionManager.DecreaseLiquidityParams({
                tokenId: tokenId,
                liquidity: liquidity,
                amount0Min: 0,
                amount1Min: 0,
                deadline: block.timestamp
            });
    
        // Remove liquidity
        return nonfungiblePositionManager.decreaseLiquidity(params);
    }
}
```
