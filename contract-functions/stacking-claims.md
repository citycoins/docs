---
description: CityCoin contract functions related to stacking claims.
---

# Stacking Claims

## Overview

After CityCoins are Stacked in the contract, Stackers are required to claim their rewards and unlocked CityCoins after a cycle ends.

Claiming rewards from Stacking CityCoins happens by calling the contract function [`claim-stacking-rewards`](stacking-claims.md#claim-stacking-reward).

## Details

The payouts are based on the amount Stacked by the user `R`, the total STX reward that cycle `S`, and the total of all Stackers`T`using the formula:\
`STX Rewards = (R * S) / T`

## Contract Functions

### claim-stacking-reward

Type: Public Function

Input: `targetCycle as uint`

Success: `(ok true)`

Errors:

* `ERR_USER_ID_NOT_FOUND u1003`
* `ERR_STACKING_NOT_AVAILABLE u1015`
* `ERR_REWARD_CYCLE_NOT_COMPLETED u1017`
* `ERR_NOTHING_TO_REDEEM u1018`

Claiming Stacking rewards happens through calling the `claim-stacking-reward` function in the contract, which accepts a reward cycle and checks both the entitled STX reward from miners and the amount of CityCoins to return, then transfers them to the user.
