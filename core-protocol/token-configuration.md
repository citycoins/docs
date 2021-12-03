---
description: An overview of the token component of the CityCoins protocol.
---

# Token Configuration

## Overview

The token exists separate from the core contract as part of the CityCoins Token Protocol, however there are some functions used by the core contract to interact with the token.

In addition to those functions, the token contract fully supports the [SIP-010 fungible token standard](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md) on the Stacks blockchain.

## Issuance Schedule

Miners receive coinbase rewards for mining CityCoins outlined in the table on this page per block.

The issuance schedule does not begin until [mining is activated](broken-reference), and once it begins, the current block height of the Stacks blockchain is recorded in the smart contract.

From there, the amount of CityCoins rewarded through mining follow a similar issuance schedule to that of Bitcoin and Stacks, where the mining rewards are cut in half over the next 20 years.

**Please note:** there is a 10,000 block bonus reward for early miners who support the initiative.

| Time Period                   | Rewards           | Notes                               |
| ----------------------------- | ----------------- | ----------------------------------- |
| First 10,000 Stacks blocks    | 250,000 CityCoins | approx. 3 months                    |
| Next 200,000 Stacks blocks    | 100,000 CityCoins | approx. 4 years, minus bonus period |
| Next 210,000 Stacks blocks    | 50,000 CityCoins  | approx. 4 years                     |
| Next 210,000 Stacks blocks    | 25,000 CityCoins  | approx. 4 years                     |
| Next 210,000 Stacks blocks    | 12,500 CityCoins  | approx. 4 years                     |
| Next 210,000 Stacks blocks    | 6,250 CityCoins   | approx. 4 years                     |
| After 1,050,000 Stacks blocks | 3,125 CityCoins   | continues indefinitely              |

After the final halving at 1,050,000 Stacks blocks past the Stacks block height recorded at activation, the total supply is estimated to be 42,187,500,000 CityCoins and will increase indefinitely by up to 164,062,500 CityCoins per year.
