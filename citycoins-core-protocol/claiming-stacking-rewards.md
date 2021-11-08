# Claiming Stacking Rewards

## Overview

While Stacking CityCoins is similar to Stacking STX, there are a few key differences.

Instead of rewards being delivered automatically during the cycle, Stackers must wait for the **reward cycles to pass** before claiming their Stacking rewards, which consist of:

* the Stacks (STX) sent by miners
* the amount of CityCoins they Stacked, if unlocked

For example, if you Stacked CityCoins for three cycles starting in Cycle 1, then you would be able to claim:

* your portion of the 70% Stacks (STX) sent by miners for Cycle 1, after Cycle 1 ends
* your portion of the 70% Stacks (STX) sent by miners for Cycle 2, after Cycle 2 ends
* your portion of the 70% Stacks (STX) sent by miners for Cycle 3, in addition to the Stacked CityCoins, after Cycle 3 ends

Each Stacker receives rewards proportionate to what they stacked against the total amount of Stacked CityCoins for the given reward cycle.

The payouts are based on the amount Stacked by the user `S`, the total STX reward that cycle `R`, and the total of all Stackers`T`using the formula:\
`STX Rewards = (R * S) / T`

## Related Contract Functions

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

