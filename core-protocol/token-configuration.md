---
description: An overview of the token component of the CityCoins protocol.
---

# Token Configuration

{% hint style="info" %}
CityCoins require the [Stacks Web Wallet](https://hiro.so/wallet/install-web) to interact with the smart contracts on the [Stacks blockchain](https://stacks.co). (see [How do I get started?](../about-citycoins/how-do-i-get-started.md))
{% endhint %}

## Overview

CityCoins are fungible tokens on the Stacks blockchain with no ICO, no pre-sale, and no pre-mine.

Once a CityCoin is deployed and [activated](registration-and-activation.md), the emission schedule begins and winning miners mint the CityCoin into existence.

CityCoins can be sent and received using a STX address, used for payment in smart contracts, and more.

For a more technical explanation, please see the contract functions for [CityCoins tokens](../contract-functions/token.md).

## Emissions Schedule

Miners receive coinbase rewards for mining CityCoins outlined in the table on this page **per block**.

The emission schedule does not begin until [mining is activated](registration-and-activation.md#overview), and once it begins, the current block height of the Stacks blockchain is recorded in the smart contract.

From there, the amount of CityCoins rewarded through mining follow a [doubling epoch halving schedule](https://github.com/citycoins/governance/blob/main/ccips/ccip-008/ccip-008-citycoins-sip-010-token-v2.md#emissions-schedule), where the mining rewards are cut in half in intervals over the next 20 years.

{% hint style="info" %}
There is a bonus block reward for early miners who participate in the first 10,000 blocks.
{% endhint %}

| <p>Time Period<br>(Stacks Blocks)</p> | Rewards (CityCoins) | Notes                                        |
| ------------------------------------- | ------------------- | -------------------------------------------- |
| First 10,000                          | 250,000             | \~3 months                                   |
| Next 35,000                           | 100,000             | \~8 months                                   |
| Next 85,000                           | 50,000              | \~20 months                                  |
| Next 185,000                          | 25,000              | \~3.5 years                                  |
| Next 385,000                          | 12,500              | \~7.4 years                                  |
| Next 785,000                          | 6,250               | \~15.1 years                                 |
| After 1,585,000                       | 3,125               | <p>~30.5 years<br>continues indefinitely</p> |

After the final halving at 1,050,000 Stacks blocks past the Stacks block height recorded at activation, the total supply is estimated to be 17,500,000,000 CityCoins and will increase indefinitely by up to 164,062,500 CityCoins per year.

{% hint style="info" %}
The values above are denoted in CityCoins, and the values in the contract and APIs the value will represent the reward/supply above multiplied by `1,000,000` to account for the 6 decimal places as micro-CityCoins.
{% endhint %}
