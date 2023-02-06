# Blueberry contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Resources

- [website](https://blueberry.garden)
- [Twitter](https://twitter.com/blbprotocol)
- [Medium](https://medium/@blueberryprotocol)
- [docs](https://docs.blueberry.garden)
- [Detailed Documentation](https://drive.google.com/drive/u/2/folders/1VEJzBm05IWJdF3gT4i32p4vNl11dGkx-)

# On-chain context

```
DEPLOYMENT: mainnet
LANGUAGE: solidity 0.8.16
ERC20: [any]
ERC721: [any]
ERC777: [any]
ADMIN: [trusted]
```

The Admin is set to the multisig wallet for the protocol. The multisig requires a super majority for any transaction to take place. The admin will always be a multi-sig. During the early days the safeguards that are put in place are set to protect the protocol's solvency and longevity. Over time the protocol will shift into being more permissionless. 
In case of restricted, by default Sherlock does not consider direct protocol rug pulls as a valid issue unless the protocol clearly describes in detail the conditions for these restrictions. 
For contracts, owners, admins clearly distinguish the ones controlled by protocol vs user controlled. This helps watsons distinguish the risk factor. 
Example: 
* `ContractA.sol` is owned by the protocol. 
* `admin` in `ContractB` is restricted to changing properties in `functionA` and should not be able to liquidate assets or affect user withdrawals in any way. 
* `admin` in `ContractC` is user admin and is restricted to only `functionB`

# Audit scope
[Github](https://github.com/sherlock-audit/2023-02-blueberry)

```
Includes:
    - All contracts in `/contracts`
```

# About {Blueberry}
Blueberry is a multi step yield aggregator with an initial focus on Uni v3 automated management strategies. Blueberry interacts with it’s own money market (Compound fork), where we are able to allow for borrowing in a more capital efficient manner than others on-chain, as loans are now able to be evaluated for their specific deployment. In order to allow greater capital efficiency for borrowers (up to 600% LTV in certain cases), blueberry sets risk parameters such as LTV and min/max Position Size based on the specific deployment.

The deployment is called a "spell." A spell can be anything that can be priced and has adequate liquidity, from Uniswap v3 management vaults to leverage longing Ethereum.

Risk parameters are set by the DAO in cooperation with security consultants who analyze on chain liquidity data to ensure safety.

This design requires a level of discretion and trust in the DAO that may appear more risky than it is at first glance, as the bank can borrow without restriction in order to enable spells.

Another unique feature of blueberry is its isolated collateral. In other leverage protocols, the position is considered the collateral itself.

On Blueberry, the mechanism is designed more like a leverage trading exchange, where the PNL of the trade (the spell/deployment in Blueberry's case) is measured against the collateral provided.

This separation allows more flexible strategies for users. For example, a user might want to hold WBTC while leverage farming the ETH-stETH arb, to keep price exposure in BTC while earning a yield.

# Steps to run the tests:
Hardhat version 2.12.4 Block height 16283930 Eth mainnet fork

1. Clone the repo
2. `npm install`
3. Create .env file with env var `DEPLOY_ACCOUNT_KEY=` , `ALCHEMY_API_KEY=` , `ETHERSCAN_API_KEY=` (use http://alchemy.com)
4. `npx hardhat compile`
5. `npx hardhat test`
6. `npx hardhat coverage`