# Mining CityCoins

## Description

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
  
There is a maximum of 128 miners per block, however once that threshold is reached, additional miners can still submit a bid subject to the following rules:

* if the bid is lower than the lowest bid of the 128 miners, then the bid is rejected and the transaction fails
* if the bid is higher than the lowest bid of the 128 miners, then the lowest bidder is pushed out from the list

**Please note: Miners who has been pushed out of the list are not taking part of the winner selection and their commitment is not refundable.**

