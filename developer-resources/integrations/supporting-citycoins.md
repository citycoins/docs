---
description: Interacting with the CityCoins protocol.
---

# Supporting CityCoins

## CityCoins Contracts

Each CityCoin is defined by a set of contracts for that city, including `core`, `token`, and `auth`.

The [Contracts page](../citycoin-contracts.md) lists the currently deployed CityCoins contracts with links to their on-chain source. The [GitHub repo](https://github.com/citycoins/citycoin/tree/main/contracts) is where the contracts are stored and updated before deployment.

## SIP-010 Standard

[SIP-010: Standard Trait Definition for Fungible Tokens](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md)

> Clarity, has built-in language primitives to define and use fungible tokens. Although those primitives exists, there is value in defining a common interface (known in Clarity as a "trait") that allows different smart contracts to interoperate with fungible token contracts in a reusable way. This SIP defines that trait.

SIP-010 includes function definitions for:

* transfer
* name (human-readable)
* symbol (ticker)
* decimals (CityCoins have 6)
* balance
* total supply
* token URI (externally hosted metadata)

## Send-Many Function

In addition to SIP-010, all CityCoins token contracts implement an additional `citycoin-token` trait that defines:

* activation
* set token URI
* mint
* burn
* send-many

The send-many function allows for sending to a list of up to 200 recipients in a single transaction.

The list must contain at least one entry with the following values:

* to: principal
* amount: uint
* memo: optional buff 34

## Token Metadata

[Metadata for CityCoins](https://github.com/citycoins/cdn/tree/main/cdn/metadata) are stored in a CDN available at [https://cdn.citycoins.co](https://cdn.citycoins.co/).

[MiamiCoin (MIA) example](https://cdn.citycoins.co/metadata/miamicoin.json):&#x20;

```
{
  "name": "MiamiCoin",
  "description": "A CityCoin for Miami, ticker is MIA, Stack it to earn Stacks (STX)",
  "image": "https://cdn.citycoins.co/logos/miamicoin.png"
}
```

## Brand Resources

More information on brand assets and guidelines for CityCoins can be found in the [CityCoins Resources](broken-reference) section.

## Stacking CityCoins

CityCoins follow a similar protocol to [Stacking STX](https://github.com/citycoins/integrations/blob/main/README.md#stacking-stx) with a few key differences.

In the Stacks blockchain, 100% of what Stacks miners spend in BTC is transferred to Stackers.

In the CityCoins protocol, 30% of what CityCoin miners spend in STX is transferred to the custodied city wallet, and the remaining 70% is transferred to Stackers.

* Stacked CityCoins are transferred to the contract for the duration of the cycles
  * STX rewards for each cycle can be claimed after the cycle ends
  * Stacked CityCoins can be reclaimed after the final cycle ends
* Stacking rewards are distributed proportionately to the amount stacked, not in reward slots
* Reward cycles are also 2,100 Stacks blocks in length, but the maximum is 32 cycles

Additional common questions and answers can be found in the [Stacking Documentation](../../core-protocol/stacking-citycoins.md#common-questions).
