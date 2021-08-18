# Stacking CityCoins

## Overview

Stacking CityCoins is performed by transferring CityCoins into the smart contract for a selected number of reward cycles. Reward cycles are 2,100 Stacks blocks in length \(about two weeks\), similar to Stacking STX.

When Stacking, you must select:

* the amount of CityCoins you want to Stack, which will be sent to the smart contract
* the number of reward cycles you want to participate in, maximum 32

**Please note:** the block height chosen for Stacking will automatically select the _next reward cycle_ to start Stacking CityCoins.

_e.g. if you select to Stack in a block height in reward cycle 1 then Stacking will begin in reward cycle 2._

You cannot Stack in the currently active reward cycle, only for the next reward cycle.

## Reward Cycles

| Reward Cycle | Start Block | End Block |
| :--- | :--- | :--- |
| 0 | 24497 | 26596 |
| 1 | 26597 | 28696 |
| 2 | 28697 | 30796 |
| 3 | 30797 | 32896 |
| ...and so on at | 2,100 blocks | per cycle |

The current reward cycle for a given block height can be found by calling `get-reward-cycle` in the contract and supplying the block height.

## **Common Questions**

**Q: Do the Stacked CityCoins stay in my wallet?**

A: No, they are transferred to the contract, and can be reclaimed once the stacking cycle is complete. Some examples are below.

* if you Stack 50,000 CityCoins for 1 cycle, then after the cycle ends you can claim the STX rewards for that cycle in addition to the 50,000 CityCoins
* if you Stack 50,000 CityCoins for 3 cycles, then after cycle 1 and 2 you can claim the STX rewards for each, and after cycle 3 you can claim the STX rewards in addition to the 50,000 CityCoins

**Q: Is there a minimum amount for Stacking?**

A: No, however the STX rewards for a given cycle are proportionate to the amount you Stack versus the total Stacked in that cycle. If the amount you Stack in CityCoins entitles you to less than 1 uSTX \(0.000001 STX\) then no reward will be received.

**Q: Can I change the duration of CityCoins I've already Stacked?**

A: No, once `stack-tokens` is called the CityCoins are transferred to the smart contract and the values are set.

**Q: Is there a "cooldown" between cycles?**

A: Yes, when you are finished Stacking and reclaim your CityCoins, you can then stack for the _next cycle_. For example, with MiamiCoin \(MIA\):

* A user submits a Stacking transaction at block height \#26386 for one cycle
* Since block \#26836 is part of Cycle 0, the MIA are Stacked for Cycle 1
* After Cycle 1 finishes at \#28696, the user can reclaim their STX rewards and their Stacked MIA
* The user submits a Stacking transaction at block height \#28697 for one cycle
* Since block \#28697 is part of Cycle 2, the MIA are Stacked for Cycle 3
* After Cycle 3 finishes at \#32896, the user can reclaim their STX rewards and their Stacked MIA

**Q: Can I Stack additional tokens for a cycle?**

A: Yes, if you call the `stack-tokens` function before the block height of the next cycle, you can add to the amount Stacked as well as choose different amounts for a different number of cycles. In a more complex example:

* the user has 1,000,000 CityCoins to Stack
* the user calls `stack-tokens` during cycle 0 with 250,000 for 1 cycle
* the user calls `stack-tokens` during cycle 0 with 250,000 for 1 cycle
* the user calls `stack-tokens` during cycle 0 with 500,000 for 3 cycles
* the payouts would then be based on the amount Stacked by the user `S`, the total STX reward that cycle `R`, and the total of all Stackers `T`using the formula: `STX Rewards = (R * S) / T`

| Reward Cycle | Amount Stacked | Claimable Amount | STX Rewards |
| :--- | :--- | :--- | :--- |
| 0 | none | none | none |
| 1 | 1,000,000 CityCoins | 500,000 CityCoins | `(R * 1,000,000) / T` |
| 2 | 500,000 CityCoins | 0 CityCoins | `(R * 500,000) / T` |
| 3 | 500,000 CityCoins | 0 CityCoins | `(R * 500,000) / T` |
| 4 | none | 500,000 CityCoins | none |

## Related Contract Functions

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

\`\`

