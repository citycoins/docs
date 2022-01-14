---
description: CityCoin contract functions related to mining.
---

# Mining

## Overview

Anyone can create a user interface for mining a CityCoin, two examples being [minecitycoins.com](https://minecitycoins.com) and [minemiamicoin.com](https://minemiamicoin.com).

Mining CityCoins happens by calling one of two functions in the contract: `mine-tokens` and `mine-many`.

{% hint style="warning" %}
Miners can only participate once per block. Once STX are sent for mining a CityCoin **they are not returned,** they are distributed to the city's wallet and CityCoin Stackers.
{% endhint %}

A nominal transaction fee is required in order to send this transaction, paid in STX, and in a single mining transaction you can optionally include a memo that will be recorded on-chain.

## Details

To mine for a single block with `mine-tokens`:

* enter the amount you would like to bid for the block
* (optionally) enter a memo to be recorded on chain
* submit the transaction to the smart contract

To mine for multiple blocks with `mine-many`:

* select the number of blocks you would like to mine for
* enter the amount for each of the number of blocks selected
* submit the transaction to the smart contract

## Contract Functions

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
