---
description: An overview of the mining component of the CityCoins protocol.
---

# Mining CityCoins

## Overview

Anyone can mine CityCoins by forwarding STX into a CityCoins smart contract on the Stacks blockchain. Miners can only participate once per block, **and STX sent to the contract are not returned.**

Once the STX tokens are sent into the contract, they are distributed in one of two ways:

* if there are people Stacking CityCoins, then 70% is sent to Stackers and 30% is sent to the custodied wallet for the city
* if nobody is Stacking CityCoins, then 100% is sent to the custodied wallet for the city

{% hint style="info" %}
Right after mining is activated and during the first reward cycle (reward cycle #0), 100% of all STX sent by miners is transferred to the city.



During this time, CityCoins can be stacked for the next reward cycle, and following this initialization period Stacking will be available indefinitely. **** See the [Stacking section](stacking-citycoins.md#overview) for more detail.
{% endhint %}

## Details

Anyone can create a user interface for mining a CityCoin, two examples being [minecitycoins.com](https://minecitycoins.com) and [minemiamicoin.com](https://minemiamicoin.com).

Mining CityCoins happens by calling one of two functions in the contract: `mine-tokens` and `mine-many`.

{% hint style="warning" %}
Once STX are submitted in a mining transaction, they are not returned, they are distributed to the city's custodied wallet and Stackers of a CityCoin.
{% endhint %}

A nominal transaction fee is required in order to send this transaction, paid in STX, and in a single mining transaction you can optionally include a memo that will be recorded on-chain.

To mine for a single block with `mine-tokens`:

* enter the amount you would like to bid for the block
* (optionally) enter a memo to be recorded on chain
* submit the transaction to the smart contract

To mine for multiple blocks with `mine-many`:

* select the number of blocks you would like to mine for
* enter the amount for each of the number of blocks selected
* submit the transaction to the smart contract

## **Winner Selection**

After miners send their STX to the contract, a winner is selected by a Verifiable Random Function (VRF) weighted by the individual miners' bid compared to the total miners' bids sent in that block.

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

An example with real numbers: the table below assumes the total committed by miners is 500 STX, and you have 200 STX to spend.

|          |                  |             |
| -------- | ---------------- | ----------- |
| Spend    | Number of Blocks | Probability |
| 1 STX    | 200              | 32.9%       |
| 10 STX   | 20               | 32.7%       |
| 12.5 STX | 16               | 32.6%       |
| 100 STX  | 2                | 30.5%       |
| 200 STX  | 1                | 28.5%       |



## Claiming Mining Rewards

Miners must wait for a maturity window of 100 blocks (\~16 hours) before they can claim their tokens in order to protect the VRF seed. After this window passes miners can claim their rewards at any time.

{% hint style="info" %}
CityCoins are not minted until miners claim them, and therefore the total supply will only increase when miners claim their CityCoins.
{% endhint %}

If the user won the block, the transaction will succeed and mint them the block reward per the [Issuance Schedule](token-configuration.md#issuance-schedule).

{% hint style="warning" %}
If a user did not win the block, the transaction will fail.

Optionally, a user can call the `is-block-winner` and `can-claim-mining-reward` functions to see if their address can claim a given block before submitting the claim transaction.
{% endhint %}
