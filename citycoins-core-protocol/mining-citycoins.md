# Mining CityCoins

## Overview

Mining CityCoins is performed by transferring Stacks \(STX\) tokens into the smart contract in a given Stacks block, **and is a one-way process**. Once sent, the STX are committed to the contract and not returned. Miners can only participate once per block.

Once the STX tokens are sent into the contract, they are distributed in one of two ways:

* if there are people Stacking CityCoins, then 70% of the bid is sent to Stackers and 30% of the bid is sent to the custodied wallet for the city
* if nobody is Stacking CityCoins, then 100% of the bid is sent to the custodied wallet for the city

‍**Please note: Right after mining is activated and during the first reward cycle \(reward cycle \#0\), 100% of all STX sent by miners is transferred to the city.** During this time, CityCoins can be stacked for the next reward cycle, and following this initialization period Stacking will be available indefinitely.

## Details

Mining CityCoins is available through the [hosted user interface](https://minemiamicoin.com) and mining began at [block \#24497](https://explorer.stacks.co/blocks?chain=mainnet).

Mining CityCoins happens by calling one of two functions in the contract: `mine-tokens` and `mine-many`.

A nominal transaction fee is required in order to send this transaction, paid in STX, and in a single mining transaction you can optionally include a memo that will be recorded on-chain.

To mine for a single block with `mine-tokens`:

* enter the amount you would like to bid for the block
* \(optionally\) enter a memo to be recorded on chain
* submit the transaction to the smart contract

To mine for multiple blocks with `mine-many`:

* select the number of blocks you would like to mine for
* enter the amount for each of the number of blocks selected
* submit the transaction to the smart contract

_Note: once STX are submitted to the contract they are distributed to the city's custodied wallet and Stackers of MiamiCoin._

## **Winner Selection**

After miners send their STX to the contract, a winner is selected by a Verifiable Random Function \(VRF\) weighted by the individual miners' bid compared to the total miners' bids sent in that block.

_e.g. if Alice sends 10 STX into the contract and Bob sends 30 STX, then Alice has a 25% chance and Bob has a 75% chance to win in that block._

Mining rewards cannot be claimed until a 100 block maturity window passes, for more info see [Claiming Mining Rewards](claiming-mining-rewards.md).

## **Mining Strategy**

You can only submit a mining bid once per block. Once that transaction confirms then the bid is locked in.

You can optionally mine for multiple blocks in one transaction, by selecting the amount to send per block and submitting the total bid up front. Once that transaction confirms then the bid is locked in for the following blocks.

_Note: you can mine for up to 200 blocks based on the function in the contract, however due to how costs are calculated per block the transaction may fail. It is recommended to submit for less than 100 blocks._

If you submit a mining transaction in a block where you are already mining, it will fail.

The probability to win at least one block in a sequence of blocks with a fixed commit of `C` STX and a total of other miners `T` STX is the following:

```text
P(win at least 1 block in N blocks) = 1 - (T / (T + C)) ^ N
```

An example in real numbers: commit of other miners is 500 STX, and you have 200 STX to spend.

* Spending 1 STX of 200 blocks P = 32.9%
* Spending 10 STX of 20 blocks P = 32.7%
* Spending 15 STX in 16 blocks: P = 37.6%
* Spending 100 STX in 2 blocks P =  30.5%
* Spending 200 STX in 1 block:  P = 28.5%

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

