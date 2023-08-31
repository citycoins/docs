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

<table data-header-hidden><thead><tr><th width="150">Time Period</th><th width="150">Rewards</th><th width="163">Notes</th><th width="150"></th></tr></thead><tbody><tr><td>Epoch</td><td>Epoch Length</td><td>Epoch End Block</td><td>Block Reward</td></tr><tr><td>0</td><td>10,000</td><td>10,000</td><td>250,000</td></tr><tr><td>1</td><td>25,000</td><td>35,000</td><td>100,000</td></tr><tr><td>2</td><td>50,000</td><td>85,000</td><td>50,000</td></tr><tr><td>3</td><td>100,000</td><td>185,000</td><td>25,000</td></tr><tr><td>4</td><td>200,000</td><td>385,000</td><td>12,500</td></tr><tr><td>5</td><td>400,000</td><td>785,000</td><td>6,250</td></tr><tr><td>6</td><td>n/a</td><td>n/a</td><td>3,125</td></tr></tbody></table>

After the final halving the total supply is estimated to be 17,500,000,000 CityCoins and will increase indefinitely by an estimated 164,062,500 CityCoins per year.

{% hint style="info" %}
The values above are denoted in CityCoins, and the values in the contract and APIs the value will represent the reward/supply above multiplied by `1,000,000` to account for the 6 decimal places as micro-CityCoins.
{% endhint %}

### Decimals

CityCoins have 6 decimals, denoted with `u` for `micro-`.

<table><thead><tr><th width="189">Currency</th><th>Unit</th></tr></thead><tbody><tr><td>Bitcoin</td><td>1 BTC = 100,000,000 Satoshis</td></tr><tr><td>Stacks</td><td>1 STX = 1,000,000 micro-STX (uSTX)</td></tr><tr><td>CityCoins</td><td>1 CityCoin = 1,000,000 micro-CityCoin</td></tr><tr><td>MiamiCoin</td><td>1 MIA = 1,000,000 uMIA</td></tr><tr><td>NewYorkCityCoin</td><td>1 NYC = 1,000,000 NYC</td></tr></tbody></table>

Since CityCoins have 6 decimals, there will be places that may show the balance of `CityCoins * 1,000,000`. **This is not a bug.**

What's showing is the "raw" value on-chain, which represents micro-CityCoins. Consider a `50,000 MIA` block reward - claiming from the contract will mint `50,000,000,000 uMIA` which is then displayed correctly in wallets based on the number of decimals.

You can also see this in V1 to V2 conversion transactions, where for example, `50 MIA (V1)` is burned and `50,000,000 uMIA (V2)` minted, and both are equivalent in value because V2 MIA has 6 decimal places.
