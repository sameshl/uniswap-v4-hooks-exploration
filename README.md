# uniswap-v4-hooks-exploration

#### TLDR: This repo is for experimenting with different approaches to minimising loss-vs-rebalancing (LVR or lever) in CFMMs (Uni v4)

## Background:
LVR has been formulated as a better benchmark than the usual impermanent loss to monitor LP profitability on AMMs. It's essentially the loss accrued by LPs against a *rebalancing strategy*. 

```
LP Profit = Trading Fees Earned - LVR
```

By design, AMMs will **always** trade at worse-than-market (CEX) prices, leading to profits for arbitrageurs. This happens when arbitrageurs "snipe" the AMMs to recalibrate them to trade at market prices. This leak is also termed "slippage costs".

LVR is basically a zero-sum cost paid to intermediaries (arbitrageurs)! Reducing LVR will increase gains from the trade, leading to more trade activity and thus it's essentially social welfare.

Previously, AMM experimentation has been difficult with various costs related to building "externally" to Uniswap. Now, with the introduction of Hooks in Uniswap v4, we can create better AMMs (technically, pools) with the specialised features we need.

## How can we create better AMMs?

### Focus: Reduce LVR for LPs

#### Idea 1: Balance trading fees with LVR
Aggregate trading fees should be commensurate with LVR. Since, LVR changes based on market conditions, this suggests we could have dynamic fees (previously not possible in Uni v3).
The dynamic fees could be based on several factors including market volatility/variance. We could also get compare LVR versus fee income in a backwards-looking window, increasing fees if they are below LVR, and decreasing fees if they are above LVR.

#### Idea 2: Oracle AMMs
Access to reliable & high-frequency price oracle could in principle quote prices arbitrarily close to market prices, thus eliminating losses from price slippage and achieving payoffs arbitrarily close to that of the rebalancing strategy. 

#### Idea 3: try to "capture" expected LVR
The basic idea is to incorporate mechanisms for the AMM (not arbitrageurs) to "capture" the LVR and then redistribute the profits to LPs

### Focus: LP profitability

#### Idea 1: LP yield stratergies to offset LVR
Increasing yield for LP by building hooks that store extra liquidity from lending pools into lending protocol. Note that, this does have the guarantee that it will be executed/included in the contract at the time of the swap as these happen with hooks and not externally.

## Progress
We have started with designing pools with dynamic fees which are based on market prices.



