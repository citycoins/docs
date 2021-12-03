---
description: An overview of the stacking component of the CityCoins protocol.
---

# Stacking CityCoins

## Overview

Anyone can Stack CityCoins by locking them in a CityCoins smart contract for determined reward cycles, and receive a portion of the remaining 70% of the STX sent by miners.

Reward cycles are 2,100 Stacks blocks in length (\~ 2 weeks), similar to Stacking STX.

**When Stacking, you must select:**

* the amount of CityCoins you want to Stack, which will be sent to the smart contract
* the number of reward cycles you want to participate in, maximum 32 (\~16 months)

{% hint style="info" %}
You cannot Stack in the currently active reward cycle, only for the next reward cycle.

_e.g. if you select to Stack in a block height in reward cycle 1 then Stacking will begin in reward cycle 2._
{% endhint %}

The current reward cycle for a given block height can be found by calling `get-reward-cycle` in the core contract and supplying the block height.

## **Stacking Claims**

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

## **Common Questions**

### **Do the Stacked CityCoins stay in my wallet?**

No, they are transferred to the contract, and can be reclaimed once the selected cycles are complete. Some examples are below.

* if you Stack 50,000 CityCoins for 1 cycle, then after the cycle ends you can claim the STX rewards for that cycle in addition to the 50,000 CityCoins
* if you Stack 50,000 CityCoins for 3 cycles, then after cycle 1 and 2 you can claim the STX rewards for each, and after cycle 3 you can claim the STX rewards in addition to the 50,000 CityCoins

### **Is there a minimum amount for Stacking?**

No, however the STX rewards for a given cycle are proportionate to the amount you Stack versus the total Stacked in that cycle.

If the amount you Stack in CityCoins entitles you to less than 1 uSTX (0.000001 STX) then no reward will be received.

### **Can I change the duration of CityCoins I've already Stacked?**

No, once `stack-tokens` is called the CityCoins are transferred to the smart contract and the values are set. There is no way to update it.

### **Is there a cooldown between cycles?**

Yes, when you are finished Stacking and reclaim your CityCoins, you can then stack for the _next cycle_. An example with MiamiCoin (MIA):

* A user submits a Stacking transaction at block height #26386 for one cycle
* Since block #26386 is part of Cycle 0, the MIA are Stacked for Cycle 1
* After Cycle 1 finishes at #28696, the user can reclaim their STX rewards and their Stacked MIA
* The user submits a Stacking transaction at block height #28697 for one cycle
* Since block #28697 is part of Cycle 2, the MIA are Stacked for Cycle 3
* After Cycle 3 finishes at #32896, the user can reclaim their STX rewards and their Stacked MIA

### **Can I Stack additional tokens for a cycle?**

A: Yes, if you call the `stack-tokens` function before the next cycle starts, you can add to the amount Stacked as well as choose different amounts for a different number of cycles.

In a more complex example:

* the user has 1,000,000 CityCoins to Stack
* the user calls `stack-tokens` during cycle 0 with 250,000 for 1 cycle
* the user calls `stack-tokens` during cycle 0 with 250,000 for 1 cycle
* the user calls `stack-tokens` during cycle 0 with 500,000 for 3 cycles

The payouts would then be based on the amount Stacked by the user `S`, the total STX reward that cycle `R`, and the total of all Stackers `T`using the formula: `STX Rewards = (R * S) / T`

| Reward Cycle | Amount Stacked      | Claimable Amount  | STX Rewards           |
| ------------ | ------------------- | ----------------- | --------------------- |
| 0            | none                | none              | none                  |
| 1            | 1,000,000 CityCoins | 500,000 CityCoins | `(R * 1,000,000) / T` |
| 2            | 500,000 CityCoins   | 0 CityCoins       | `(R * 500,000) / T`   |
| 3            | 500,000 CityCoins   | 0 CityCoins       | `(R * 500,000) / T`   |
| 4            | none                | 500,000 CityCoins | none                  |
