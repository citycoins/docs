# Claiming Mining Rewards

## Overview

Miners must wait for a maturity window of 100 blocks \(~16 hours\) before they can claim their tokens in order to protect the VRF seed. After this window passes miners can claim their rewards at any time.  
  
‍**Please note:** CityCoins are not minted until miners claim them, and therefore the total supply will only increase when miners claim their CityCoins.

## Details

Claiming mining rewards for CityCoins is available through the [hosted user interface](https://minemiamicoin.com).

If a user is a winner for that block, the transaction will succeed and mint them the block reward per the [Issuance Schedule](issuance-schedule.md).

_Note: If a user is not the winner for a block, the transaction will fail. Optionally, a user can call the `is-block-winner` function to see if there address won a given block before claiming._

## Related Contract Functions

### claim-mining-reward

Type: Public Function

### is-block-winner

Type: Read-only Function

### can-claim-mining-reward

Type: Read-only Function



