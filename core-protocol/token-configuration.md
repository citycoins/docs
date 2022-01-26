---
description: An overview of the token component of the CityCoins protocol.
---

# Token Configuration

## Overview

CityCoins are fungible tokens on the Stacks blockchain with no ICO, no pre-sale, and no pre-mine.

Once a CityCoin is deployed and [activated](registration-and-activation.md), the issuance schedule begins and winning miners mint the CityCoin into existence.

CityCoins can be sent and received using a STX address, used for payment in smart contracts, and more.

For a more technical explanation, please see the contract functions for [CityCoins tokens](../contract-functions/token.md).

## Issuance Schedule

Miners receive coinbase rewards for mining CityCoins outlined in the table on this page **per block**.

The issuance schedule does not begin until [mining is activated](registration-and-activation.md#overview), and once it begins, the current block height of the Stacks blockchain is recorded in the smart contract.

From there, the amount of CityCoins rewarded through mining follow a similar issuance schedule to that of Bitcoin and Stacks, where the mining rewards are cut in half over the next 20 years.

{% hint style="info" %}
There is a bonus block reward for early miners who participate in the first 10,000 blocks.
{% endhint %}

| Time Period                   | Rewards           | Notes                               |
| ----------------------------- | ----------------- | ----------------------------------- |
| First 10,000 Stacks blocks    | 250,000 CityCoins | approx. 3 months                    |
| Next 200,000 Stacks blocks    | 100,000 CityCoins | approx. 4 years, minus bonus period |
| Next 210,000 Stacks blocks    | 50,000 CityCoins  | approx. 4 years                     |
| Next 210,000 Stacks blocks    | 25,000 CityCoins  | approx. 4 years                     |
| Next 210,000 Stacks blocks    | 12,500 CityCoins  | approx. 4 years                     |
| Next 210,000 Stacks blocks    | 6,250 CityCoins   | approx. 4 years                     |
| After 1,050,000 Stacks blocks | 3,125 CityCoins   | continues indefinitely              |

After the final halving at 1,050,000 Stacks blocks past the Stacks block height recorded at activation, the total supply is estimated to be 42,187,500,000 CityCoins and will increase indefinitely by up to 164,062,500 CityCoins per year.
