---
description: CityCoin contract functions related to stacking claims.
---

# Stacking Claims

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
