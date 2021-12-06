---
description: CityCoin contract functions related to stacking.
---

# Stacking

### get-stacking-stats-at-cycle

Type: Read-only Function

Input: `rewardCycle as uint`

Returns: `(some StackingStatsAtCycle) as a tuple` or `(none)`

Returns the stacking stats at a given reward cycle, including:

* `amountUstx` - total rewards from miners in uSTX
* `amountToken` - total CityCoins Stacked

### get-stacking-stats-at-cycle-or-default

Type: Read-only Function

Input: `rewardCycle as uint`

Returns: `(some StackingStatsAtCycle) as a tuple, or defaults`

Returns the same as `get-stacking-stats-at-cycle` above, except if no entry is found, returns the default structure of:

* `amountUstx: 0`
* `amountToken: 0`

### get-stacker-at-cycle

Type: Read-only Function

Input: `rewardCycle as uint` and `userId as uint`

Returns: `(some StackerAtCycle) as a tuple` or `(none)`

Returns the stacking stats for a given user ID and reward cycle, including:

* `amountStacked` - the total amount of CityCoins Stacked
* `toReturn` - the total amount of CityCoins that can be reclaimed from the contract

### get-stacker-at-cycle-or-default

Type: Read-only Function

Input: `rewardCycle as uint` and `userId as uint`

Returns: `(some StackerAtCycle) as a tuple, or defaults`

Returns the same as `get-stacker-at-cycle` above, except if no entry is found, returns the default structure of:

* `amountStacked: 0`
* `toReturn: 0`

### get-reward-cycle

Type: Read-only Function

Input: `stacksHeight as uint`

Returns: `(some rewardCycle) as uint` or `(none)`

Returns the active reward cycle for a given block height.

### stacking-active-at-cycle

Type: Read-only Function

Input: `rewardCycle as uint`

Returns: `true` or `false`

Returns a boolean value indicating if stacking is active at a given reward cycle, meaning a positive number of CityCoins are Stacked for that cycle.

### get-first-stacks-block-in-reward-cycle

Type: Read-only Function

Input: `rewardCycle as uint`

Returns: `firstBlockInCycle as uint`

Returns the starting Stacks block height for a given reward cycle.

### get-stacking-reward

Type: Read-only Function

Input: `userId as uint` and `targetCycle as uint`

Returns: `entitledStackingReward as uint, or default (u0)`

Returns the amount of STX a user can claim in a given reward cycle in uSTX. This method will only return a positive value if:

* the current block height is in a subsequent reward cycle
* the Stacker locked up CityCoins in the target reward cycle
* the Stacker locked up _enough_ CityCoins to receive at least one uSTX

### stack-tokens

Type: Public Function

Input: `amountTokens as uint` and `lockPeriod as uint`

Success: `(ok true)`

Errors:

* `ERR_CONTRACT_NOT_ACTIVATED u1005`
* `ERR_STACKING_NOT_AVAILABLE u1015`
* `ERR_CANNOT_STACK u1016`

Stacking happens through calling the `stack-tokens` function in the contract, which accepts an amount of CityCoins to Stack in addition to a number of reward cycles to Stack them for.