# Mining CityCoins

## Overview

Mining CityCoins is performed by transferring Stacks \(STX\) tokens into the smart contract in a given Stacks block, and is a one-way process. Miners can only participate once per block.

Once the STX tokens are sent into the contract, they are distributed in one of two ways:

* if there are people Stacking CityCoins, then 70% of the bid is sent to Stackers and 30% of the bid is sent to the custodied wallet for the city
* if nobody is Stacking CityCoins, then 100% of the bid is sent to the custodied wallet for the city

‍**Please note: Right after mining is activated and during the first reward cycle \(reward cycle \#0\), 100% of all STX sent by miners is transferred to the city.** During this time, CityCoins can be stacked for the next reward cycle, and following this initialization period Stacking will be available indefinitely.

## **Winner Selection**

After miners send their STX to the contract, a winner is selected by a Verifiable Random Function \(VRF\) weighted by the individual miners' bid compared to the total miners' bids sent in that block.  
  
_e.g. if Alice sends 10 STX into the contract and Bob sends 30 STX, then Alice has a 25% chance and Bob has a 75% chance to win in that block._

## **Mining Strategy**

You can only submit a mining bid once per block. Once that transaction confirms then the bid is locked in.

You can optionally mine for 30 blocks in one transaction at a given rate by submitting the total bid up front. Once that transaction confirms then the bid is locked in and distributed evenly across those 30 blocks.

If you submit a mining transaction in a block where you are already mining, it will fail.

## Related Contract Functions

### get-mining-stats-at-block

Type: Read-only Function

### get-mining-stats-at-block-or-default

Type: Read-only Function

### has-mined-at-block

Type: Read-only Function

### get-miner-at-block

Type: Read-only Function

### get-miner-at-block-or-default

Type: Read-only Function

### get-last-high-value-at-block

Type: Read-only Function

### get-block-winner-id

Type: Read-only Function

### mine-tokens

Type: Public Function

### mine-many

Type: Public Function



