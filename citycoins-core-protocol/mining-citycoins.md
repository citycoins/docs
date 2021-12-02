# Mining CityCoins

## Overview

Anyone can mine CityCoins by forwarding STX into a CityCoins smart contract on the Stacks blockchain. Miners can only participate once per block, **and STX sent to the contract are not returned.**

Once the STX tokens are sent into the contract, they are distributed in one of two ways:

* if there are people Stacking CityCoins, then 70% is sent to Stackers and 30% is sent to the custodied wallet for the city
* if nobody is Stacking CityCoins, then 100% is sent to the custodied wallet for the city

{% hint style="info" %}
Right after mining is activated and during the first reward cycle (reward cycle #0), 100% of all STX sent by miners is transferred to the city.



During this time, CityCoins can be stacked for the next reward cycle, and following this initialization period Stacking will be available indefinitely. **** See the [Stacking CityCoins section](stacking-citycoins.md) for more detail.
{% endhint %}

## Details

Anyone can create a user interface for mining a CityCoin, two examples being [minecitycoins.com](https://minecitycoins.com) and [minemiamicoin.com](https://minemiamicoin.com).

Mining CityCoins happens by calling one of two functions in the contract: `mine-tokens` and `mine-many`.

{% hint style="warning" %}
Once STX are submitted to the contract they are not returned, they are distributed to the city's custodied wallet and Stackers of a CityCoin.
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

Mining rewards cannot be claimed until a 100 block maturity window passes, see the [Claiming Mining Rewards](claiming-mining-rewards.md) for more info.

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

## Related Contract Functions

### get-mining-stats-at-block

Type: Read-only Function

Input: `stacksHeight as uint`

Returns: `(some MiningStatsAtBlock) as a tuple` or `none`

Returns the mining stats at a given block height, including:

* `minersCount` -  total miners
* `amount` -  total amount committed
* `amountToCity` - amount transferred to city wallet
* `amountToStackers` - amount transferred to $MIA Stackers
* `rewardClaimed` - true/false if reward was claimed

### get-mining-stats-at-block-or-default

Type: Read-only Function

Input: `stacksHeight as uint`

Returns: `(some MiningStatsAtBlock) as a tuple, or defaults`

Returns the same as `get-mining-stats-at-block` above, except if no entry is found, returns the default structure of:

* `minersCount: 0`
* `amount: 0`
* `amountToCity: 0`
* `amountToStackers: 0`
* `rewardClaimed: false`

### has-mined-at-block

Type: Read-only Function

Input: `stacksHeight as uint` and `userId as uint`

Returns: `true` or `false`

Returns a boolean value indicating if the user's ID mined at a given block height.

### get-miner-at-block

Type: Read-only Function

Input: `stacksHeight as uint` and `userId as uint`

Returns: `(some MinersAtBlock) as a tuple` or `(none)`

Returns the mining stats for a given user ID and block height, including:

* `ustx` - total commitment in uSTX
* `lowValue` - used by VRF to determine winner
* `highValue` - used by VRF to determine winner
* `winner` - true/false updated _after_ miner claims the reward

### get-miner-at-block-or-default

Type: Read-only Function

Input: `stacksHeight as uint` and `userId as uint`

Returns: `(some MinersAtBlock) as a tuple, or defaults`

Returns the same as `get-miner-at-block` above, except if no entry is found, returns the default structure of:

* `ustx: 0`
* `lowValue: 0`
* `highValue: 0`
* `winner: false`

### get-last-high-value-at-block

Type: Read-only Function

Input: `stacksHeight as uint`

Returns:`highValue as uint, or default (u0)`

Returns the last high value at a given block height, which is incremented with each miners' total commitment.

### get-block-winner-id

Type: Read-only Function

Input: `stacksHeight as uint`

Returns:  `(some userId) as uint` or `none`

Returns the user ID of the block winner _after_ the  miner claims the reward.

### mine-tokens

Type: Public Function

Input: `amountUstx as uint` and `memo as buff 34 (optional)`

Success: `(ok true)`

Errors:

* `ERR_CONTRACT_NOT_ACTIVATED u1005`
* `ERR_USER_ALREADY_MINED u1006`
* `ERR_INSUFFICIENT_COMMITMENT u1007`
* `ERR_INSUFFICIENT_BALANCE u1008`
* `ERR_STACKING_NOT_AVAILABLE u1015`

Mining for a single block happens through calling the `mine-tokens` function in the contract, which optionally accepts up to 34 characters as a memo to record on-chain.

### mine-many

Type: Public Function

Input: `amounts as list of uints, up to 200`

Success: `(ok true)`

Errors:

* `ERR_CONTRACT_NOT_ACTIVATED u1005`
* `ERR_USER_ALREADY_MINED u1006`
* `ERR_INSUFFICIENT_COMMITMENT u1007`
* `ERR_INSUFFICIENT_BALANCE u1008`
* `ERR_STACKING_NOT_AVAILABLE u1015`

Mining for many blocks happens through calling the `mine-many` function in the contract, which accepts a list of amounts up to 200 items in length.
