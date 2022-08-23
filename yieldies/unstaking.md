# Un-staking

Users desiring to redeem yieldies for their underlying assets have a few different options depending on the asset
and their need for immediate liquidity.  

Currently, yieldies require a user to first request withdrawal of their assets prior to being able to redeem.  This is due to the fact that the underlying
assets are aren't immediately liquid and are being used in DeFi strategies to generate yield. Once the request is made the funds will become available for withdrawal
within 7-14 days.  

There are other options however if you require immediate liquidity to the underlying assets.

#### If you require immediate liquidity your options may include:

- **Instant un-staking through the Liquidity Reserve** - a Liquidity Reserve is available for each Yieldy and its associated
underlying asset. If there is sufficient liquidity in the reserve a user may swap their Yieldy for the underlying asset instantly but incur a fee in doing so. 
This fee is distributed back to the liquidity providers who have supplied the underlying asset to the pool.

- **Instant un-staking through a Curve pool** - Currently all Yieldies will leverage Tokemak for yield generation. The means that the underlying assets are deposited
to Tokemak and in turn the Staking contract is issued tAssets.  If a Curve pool for these tAssets exists, the Staking contract can facilitate instant un-staking
by swapping the tAsset for the underlying asset at the current market rate, returning the underlying asset to the user.  In this case, no fee is charged by Yieldies, and instead the swap is subject to fees and slippage on the Curve pool.

- **Trading on ElasticSwap** - Each Yieldy may additionally have a liquid secondary market on [ElasticSwap](https://elasticswap.org/) in which users may be able to swap
their Yieldy for other assets. 
