---
description: CityCoin contract functions related to mining claims.
---

# Mining Claims

## Overview

After miners send their STX to the contract, a winner is later calculated by a Verifiable Random Function (VRF) weighted by the individual miner's bid compared to the total miners' bids sent in that block_._

{% hint style="info" %}
Example 1: Alice sends 10 STX and Bob sends 30 STX in a block. The total spent for the block is 40 STX.

* Alice has a 25% chance of winning (10/40 STX)
* Bob has a 75% chance of winning (30/40 STX)
{% endhint %}

{% hint style="info" %}
Example 2: Alice sends 20 STX, Bob sends 30 STX, Carol sends 50 STX, and Dave sends 100 STX in a block. The total spent for the block is 200 STX.

* Alice has a 10% chance of winning (20/200)
* Bob has a 15% chance of winning (30/200)
* Carol has a 25% chance of winning (50/200)
* Dave has a 50% chance of winning (100/200)
{% endhint %}

Claiming a mining reward happens by calling the [`claim-mining-reward`](mining-claims.md#claim-mining-reward) function in the contract.

## Details

Miners must wait for a maturity window of 100 blocks (\~16 hours) before they can know the winner of a given block in order to protect the VRF seed.

After this window passes miners can claim their CityCoin block rewards at any time.

{% hint style="info" %}
CityCoins are not minted until miners claim them, and therefore the total supply will only increase when miners claim their CityCoins.
{% endhint %}

If the user won the block, the transaction will succeed and mint them the block reward per the [Emissions Schedule](../core-protocol/token-configuration.md#emissions-schedule).

{% hint style="warning" %}
If a user did not win the block, the transaction will fail.

Optionally, a user can call the [`is-block-winner`](mining-claims.md#is-block-winner) and [`can-claim-mining-reward`](mining-claims.md#can-claim-mining-reward) functions to see if their address can claim a given block before submitting the claim transaction.
{% endhint %}

## Functions

### claim-mining-reward

Type: Public Function

Input: `minerBlockHeight as uint`

Success: `(ok true)`

Errors:

* `ERR_USER_NOT_FOUND u1002`
* `ERR_USER_ID_NOT_FOUND u1003`
* `ERR_USER_DID_NOT_MINE_IN_BLOCK u1009`
* `ERR_CLAIMED_BEFORE_MATURITY u1010`
* `ERR_NO_MINERS_AT_BLOCK u1011`
* `ERR_REWARD_ALREADY_CLAIMED u1012`
* `ERR_MINER_DID_NOT_WIN u1013`
* `ERR_NO_VRF_SEED_FOUND u1014`
* `ERR_CLAIM_IN_WRONG_CONTRACT u1020`

Claiming mining rewards happens through calling the `claim-mining-reward` function in the contract, which accepts the block height the miner mined in, and checks if the VRF value is between the `lowValue` and `highValue` for the miner.

If the miner won the block, then the coinbase is minted for them based on block height of the claim and the [emissions schedule](../core-protocol/token-configuration.md#emissions-schedule).

### is-block-winner

Type: Read-only Function

Input: `user as principal` and `minerBlockHeight as uint`

Returns: `true` or `false`

Returns a boolean value indicating if the user's principal won at a given block height.

_Note: this function will always return false if the token maturity window of 100 blocks did not pass._

### can-claim-mining-reward

Type: Read-only Function

Input: `user as principal` and `minerBlockHeight as uint`

Returns: `true` or `false`

Returns a boolean value indicating if the user's principal won and is eligible to claim the block reward at a given block height.

_Note: this function will always return false if the token maturity window of 100 blocks did not pass._
