
# Applications

> Check out [sigmaverse.io](https://sigmaverse.io/) - *your portal to the Ergo Universe* 

## Live dApps

### [ErgoDex](https://ergodex.io)

- [ErgoLabs](https://github.com/ergolabs) Repository
- [EIP-0014: Decentalized Exchange Contracts](https://github.com/ergoplatform/eips/pull/27)
- [Single-Chain Swap Contracts (DEX basis) by Alex Chepurnoy](https://www.youtube.com/watch)

### [SigmaUSD](https://sigmausd.io)
The worlds first UTxO-based stable coin - an instantiation of the [AgeUSD protocol](https://github.com/Emurgo/age-usd). Its economic model designed in partnership between IOHK, Ergo, and Emurgo maintains the conservative settings for collateral reserves and avoids the need for liquidations. Along with that, it supports a fully decentralised stablecoin emission setup.

- [anon-real/sigma-usd](https://github.com/anon-real/sigma-usd)
- [Ergo Summit 2021 - The IOHK Perspective - Designing the AgeUSD StableCoin](https://youtu.be/zG-rxMCDIa0?t=9247)
- [Overview Video (with diagrams)](https://www.youtube.com/watch?v=O3hPEp3tzoU)
- [Building Ergo: How the AgeUSD stablecoin works](https://ergoplatform.org/en/blog/2021-02-05-building-ergo-how-the-ageusd-stablecoin-works/)

**DexyUSD**

- [Dexy: USD Simplest Stablecoin](https://www.ergoforum.org/t/dexy-usd-simplest-stablecoin-design/1430)
- [A Simplest Stablecoin?](https://www.ergoforum.org/t/a-simplest-stablecoin/413)


### [ErgoMixer](https://github.com/ergoMixer/ergoMixBack)

The first working non-custodial, programmable, non-interactive token mixer in the cryptocurrency space. Due to secret generation under the hood, it must be run as a local application. 

- [ergoMixer]([ergoMixBack](https://github.com/ergoMixer/)) repository
- [ZeroJoin: Combining Zerocoin and Coinjoin](https://ergoplatform.org/docs/CBT_2020_ZeroJoin_Combining_Zerocoin_and_CoinJoin_v3.pdf)
- [Video tutorial](https://www.youtube.com/watch?v=03_2HH82Plw)

### [Ergo Auction House](http://ergoauctions.org/#/auction/active)

- [Source code](https://github.com/anon-real/ErgoAuctionHouse)
- [v2 contracts](https://github.com/ergoplatform/eips/pull/39/files)
- [Profit-Sharing for Ergo Auctions House](https://www.ergoforum.org/t/profit-sharing-for-ergo-auctions-house/708)


### [Raffle](https://ergoraffle.com)
- [ErgoRaffle GitHub](https://github.com/ErgoRaffle/raffle-documentation)

## In Development

### ErgoFund

> In development


- [Ergo Crowdfunding CLI](https://github.com/robkorn/ergo-crowdfunding-cli) | Command-line tool which enables participating and interacting with crowdfunding campaigns on Ergo
- [Scanner](https://github.com/ergoplatform/scanner) 


### ZK Treasury

Tool for joint spendings with on-chain privacy 

- [Server](https://github.com/anon-real/DistributedSigsServer) 
- [Client](https://github.com/anon-real/DistributedSigsClient)
- ['A Collective Spending Appproach'](https://www.reddit.com/r/ergonauts/comments/ohftim/ergoteam_a_simpler_collective_spending_approach/)

### ErgoProfitSharingDapp

This service will provide a way for dapps to distribute gains among dapps' token holders.

The first user of this service will be the ErgoMixer. 

Ergomixer's income (in ERG and other tokens) is currently received by its creator, aka 'anon2020s', since it has only one stakeholder at the moment. He has announced that he is willing to create and sell some tokens shortly to obtain more stakeholders; let's call this token MIX. Later, anyone with the MIX tokens can stake them in the Profit Sharing contract and obtain the mixer's incomes proportional to their staked tokens.

So, it is NOT a way to stake ERG at first. But, it CAN BE USED in the future in some creative services to provide ERG-staking.

- [Ergo Profit Sharing dApp](https://github.com/mhssamadani/ErgoProfitSharingDapp)

**Use-cases**

- [A solution for staking](https://www.ergoforum.org/t/a-solution-for-staking/1057)
- [Paying fee in ErgoMix in primary tokens](https://www.ergoforum.org/t/paying-fee-in-ergomix-in-primary-tokens/73)
- [Profit-Sharing for Ergo Auctions House](https://www.ergoforum.org/t/profit-sharing-for-ergo-auctions-house/708)



### LETS

- [LETS start the discussion](https://ergoplatform.org/en/blog/2021-07-01-lets-start-the-discussion/)

## Tooling


### Oracles
> v2 contracts in review.

When external oracle data is posted on-chain, it needs to be encoded exactly within a transaction. Furthermore, oracle pools have many different moving parts that require transactions to be issued to move between the different stages of the pool protocol. [Oracle Core](https://github.com/ergoplatform/oracle-core) creates all of the complex transactions which post the data on-chain & run the oracle pool protocol on-chain (such as averaging data points). This comes bundled with [Oracle Pool Bootstrap](https://github.com/ergoplatform/oracle-core/tree/master/oracle-pool-bootstrap) and a [Connector Library](https://github.com/ergoplatform/oracle-core/tree/master/connectors/connector-lib). The [ada-usd-oracle](https://github.com/ergoplatform/oracle-core/blob/master/scripts/ada-usd-oracle/oracle-config.yaml) source can be seen here. Currently, only the erg-USD-oracle is live as seen in the [Oracle Pool List](https://explorer.ergoplatform.com/en/oracle-pools-list)

See this [overview](https://github.com/Emurgo/Emurgo-Research/blob/master/oracles/Oracle-Pools.md) by Robert Kornacki.

**Resources**

- [eth/usd connector](https://github.com/Luivatra/oracle-core/tree/eth-connector)
- [Ergo oracles](https://github.com/sininen-taivas/ergo-oracle) | simple command-line tool to launch oracles. Inbuilt implementations for USD/ERG, EUR/ERG, BTC/ERG, AUG/ERG (gold) prices delivery. 
- [Learn about data inputs and the truly novel innovations they bring to UTXO-based Blockchains](https://github.com/Emurgo/Emurgo-Research/blob/master/smart-contracts/Unlocking%20The%20Potential%20Of%20The%20UTXO%20Model.md)
 - [Ergo oracles](https://github.com/sininen-taivas/ergo-oracle) | simple command-line tool to launch oracles. Inbuilt implementations for USD/ERG, EUR/ERG, BTC/ERG, AUG/ERG (gold) prices delivery. See also a [forum topic with example](https://www.ergoforum.org/t/erg-usd-oracle-on-top-of-ergo/119)
  

**v2**

- [Oracle pool 2.0 contracts finalized (for initial draft).](https://github.com/ergoplatform/eips/blob/eip23/eip-0023.md)
- [Tests for oracle pool 2.0](https://github.com/scalahub/OraclePool/tree/v2/src/test/scala/oraclepool/v2)

### Misc

- [ergofaucet.org](https:/ErgoFaucet.org) ~ [Github](https://github.com/zargarzadehm/ergo-faucet)
- [ergo.watch](https://ergo.watch) | [Git](https://github.com/abchrisxyz/ergowatch)
- Various utilities are listed on [ergosites.github.io](https://ergosites.github.io/#ex2-tabs-3)
- [Token Minter](https://tokenminter.ergo.ga/)