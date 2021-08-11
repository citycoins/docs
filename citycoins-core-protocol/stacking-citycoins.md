# Stacking CityCoins

## Overview

Stacking CityCoins is performed by transferring CityCoins into the smart contract for a selected number of reward cycles. Reward cycles are 2,100 Stacks blocks in length \(about two weeks\), similar to Stacking STX.

When Stacking, you must select:

* the amount of CityCoins you want to Stack, which will be sent to the smart contract
* the number of reward cycles you want to participate in, maximum 32

**Please note:** the block height chosen for Stacking will automatically select the _next reward cycle_ to start Stacking CityCoins.

_e.g. if you select to Stack in a block height in reward cycle 1 then Stacking will begin in reward cycle 2._

You cannot Stack in the currently active reward cycle, only for the next reward cycle.

## Details

| Reward Cycle | Start Block | End Block |
| :--- | :--- | :--- |
| 0 | 24497 | 26596 |
| 1 | 26597 | 28696 |
| 2 | 28697 | 30796 |
| 3 | 30797 | 32896 |
| ...and so on at | 2,100 blocks | per cycle |

The current reward cycle for a given block height can be found by calling `get-reward-cycle` in the contract and supplying the block height.

## Related Contract Functions

### get-stacking-stats-at-cycle

Type: Read-only Function

### get-stacking-stats-at-cycle-or-default

Type: Read-only Function

### get-stacker-at-cycle

Type: Read-only Function

### get-stacker-at-cycle-or-default

Type: Read-only Function

### get-reward-cycle

Type: Read-only Function

### stacking-active-at-cycle

Type: Read-only Function

### get-first-stacks-block-in-reward-cycle

Type: Read-only Function

### get-stacking-reward

Type: Read-only Function

### stack-tokens

Type: Public Function

