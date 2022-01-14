---
description: An overview of the mining component of the CityCoins protocol.
---

# Mining CityCoins

{% hint style="info" %}
CityCoins require the [Stacks Web Wallet](https://hiro.so/wallet/install-web) to interact with the smart contracts on the [Stacks blockchain](https://stacks.co). (see [How do I get started?](../about-citycoins/how-do-i-get-started.md))
{% endhint %}

## Overview

Anyone can mine CityCoins by submitting a transaction to a CityCoins smart contract on the Stacks blockchain.

There are no hardware requirements and the protocol is open source, so anyone can build a website that interacts with it. The main website for mining/stacking CityCoins is [minecitycoins.com](https://minecitycoins.com).

{% hint style="warning" %}
Miners can only participate once per block. Once STX are sent for mining a CityCoin **they are not returned,** they are distributed to the city's wallet and CityCoin Stackers.
{% endhint %}

There are also [code examples](../developer-resources/code-examples/mining.md), [Node.js scripts](https://github.com/citycoins/scripts), and [community resources](../citycoins-resources/general.md#community-tools) built around mining.

For a more technical explanation, please see the [contract functions for mining](../contract-functions/mining.md).

## How it Works

CityCoin miners spend STX while competing to earn the CityCoin block reward, which is defined by the [token issuance schedule](token-configuration.md#issuance-schedule) and begins at 250,000 CityCoins per block.

* 30% of the STX that miners spend is sent directly to a reserved wallet for the city
* 70% of the STX that miners spend are distributed to people who stack their CityCoins (Stackers)

![How it Works](../.gitbook/assets/nyc-coin-how-it-works.gif)

The city can claim this wallet and convert their STX to USD whenever they want. They can also Stack the STX to earn BTC.

## **Winner Selection**

After miners send their STX to the contract, a winner is later selected by a Verifiable Random Function (VRF) weighted by the individual miners' bid compared to the total miners' bids sent in that block.

_e.g. if Alice sends 10 STX into the contract and Bob sends 30 STX, then Alice has a 25% chance and Bob has a 75% chance to win in that block._

Mining rewards cannot be claimed until a 100 block maturity window passes, see the [Claiming Mining Rewards section](mining-citycoins.md#claiming-mining-rewards) for more info.

## **Mining Strategy**

You can only submit a mining bid once per block. Once that transaction confirms then the bid is locked in. If you submit a mining transaction in a block where you are already mining, it will fail.

You can also mine for multiple blocks in one transaction, by selecting the amount to spend per block and submitting the total bid up front. Once that transaction confirms then the bid is locked in for the following blocks.

{% hint style="info" %}
You can mine for up to 200 blocks based on the function in the contract, however due to transaction costs, mining over 100 blocks may require a higher fee for the transaction to be processed.
{% endhint %}

The probability to win at least one block in a sequence of blocks with a fixed commit of `C` STX and a total of other miners `T` STX is the following:

```
P(win at least 1 block in N blocks) = 1 - (T / (T + C)) ^ N
```

An example with real numbers: the table below assumes the total committed by miners in a block is 500 STX, and as a miner you have 200 STX to spend.

|           |                      |                 |
| --------- | -------------------- | --------------- |
| **Spend** | **Number of Blocks** | **Probability** |
| 1 STX     | 200                  | 32.9%           |
| 10 STX    | 20                   | 32.7%           |
| 12.5 STX  | 16                   | 32.6%           |
| 100 STX   | 2                    | 30.5%           |
| 200 STX   | 1                    | 28.5%           |

## Claiming Mining Rewards

Miners must wait for a maturity window of 100 blocks (\~16 hours) before they can know the winner of a given block in order to protect the VRF seed.

After this window passes miners can claim their CityCoin block rewards at any time.

{% hint style="info" %}
CityCoins are not minted until miners claim them, and therefore the total supply will only increase when miners claim their CityCoins.
{% endhint %}

If the user won the block, the transaction will succeed and mint them the block reward per the [Issuance Schedule](token-configuration.md#issuance-schedule).

{% hint style="warning" %}
If a user did not win the block, the transaction will fail.

Optionally, a user can call the `is-block-winner` and `can-claim-mining-reward` functions to see if their address can claim a given block before submitting the claim transaction.
{% endhint %}
