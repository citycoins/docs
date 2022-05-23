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

| Epoch | Epoch Length | Epoch End Block | Block Reward |
| ----- | ------------ | --------------- | ------------ |
| 0     | 10,000       | 10,000          | 250,000      |
| 1     | 25,000       | 35,000          | 100,000      |
| 2     | 50,000       | 85,000          | 50,000       |
| 3     | 100,000      | 185,000         | 25,000       |
| 4     | 200,000      | 385,000         | 12,500       |
| 5     | 400,000      | 785,000         | 6,250        |
| 6     | n/a          | n/a             | 3,125        |

After the final halving the total supply is estimated to be 17,500,000,000 CityCoins and will increase indefinitely by an estimated 164,062,500 CityCoins per year.

{% hint style="info" %}
The values above are denoted in CityCoins, and the values in the contract and APIs the value will represent the reward/supply above multiplied by `1,000,000` to account for the 6 decimal places as micro-CityCoins.
{% endhint %}

### Decimals

CityCoins have 6 decimals, denoted with `u` for `micro-`.

| Currency        | Unit                                  |
| --------------- | ------------------------------------- |
| Bitcoin         | 1 BTC = 100,000,000 Satoshis          |
| Stacks          | 1 STX = 1,000,000 micro-STX (uSTX)    |
| CityCoins       | 1 CityCoin = 1,000,000 micro-CityCoin |
| MiamiCoin       | 1 MIA = 1,000,000 uMIA                |
| NewYorkCityCoin | 1 NYC = 1,000,000 NYC                 |

Since CityCoins have 6 decimals, there will be places that may show the balance of `CityCoins * 1,000,000`. **This is not a bug.**

What's showing is the "raw" value on-chain, which represents micro-CityCoins. Consider a `50,000 MIA` block reward - claiming from the contract will mint `50,000,000,000 uMIA` which is then displayed correctly in wallets based on the number of decimals.

You can also see this in V1 to V2 conversion transactions, where for example, `50 MIA (V1)` is burned and `50,000,000 uMIA (V2)` minted, and both are equivalent in value because V2 MIA has 6 decimal places.
