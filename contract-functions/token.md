---
description: CityCoin contract functions related to CityCoin tokens.
---

# Token

## Overview

The CityCoins token contract exists separate from the CityCoins core contract as part of the protocol, however there are some functions used by the core contract to interact with the token.

In addition to those functions, the token contract fully supports the [SIP-010 fungible token standard](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md) on the Stacks blockchain, including functions for [`transfer`](token.md#transfer), [`get-balance`](token.md#get-balance), and more.

CityCoins also support the [`send-many`](token.md#send-many) function, allowing up to 200 transfer operations to be performed in a single transaction.

## Details

### Decimals

CityCoins were designed not to use decimals or micro-units to avoid confusion.

With other cryptocurrencies, it is common to see smaller sub-divided units with a separate name. For example:

| Currency  | Unit                         |
| --------- | ---------------------------- |
| Bitcoin   | 1 BTC = 100,000,000 Satoshis |
| Stacks    | 1 STX = 1,000,000 uSTX       |
| CityCoins | 1 CityCoin = 1 CityCoin      |

### Minting

CityCoins can only be minted by a core contract as part of the mining claim process.

CityCoins are not minted until miners claim them.

### Burning

In the initial version (1.0.0) deployed for MIA, CityCoins can only be burned by the core contract, and no such functionality exists within the core contract.

In the subsequent version (1.0.1) deployed for NYC and future CityCoins, CityCoins can be burned by anyone following the same checks and balances as the transfer function.

## Contract Functions

### [API Ref: Token](https://api.citycoins.co/docs#tag/Token)

### activate-token

Type: Public Function

Input: `coreContract as principal` and `stacksHeight as uint`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`
* `ERR_TOKEN_ALREADY_ACTIVATED u2002`

A one-time use function to activate the token halving as defined in the [emissions schedule](../core-protocol/token-configuration.md#emissions-schedule) at a given Stacks block height. This function must be called by an active core contract, and once called, cannot be used again.

### get-coinbase-thresholds

_Note: this function is available both in the CityCoin core contract and the CityCoin token contract._

Type: Read-only Function

Input: `none`

Returns: `(ok (coinbaseThresholds)) as a tuple` or `error`

Errors:

* citycoin-core: `ERR_CONTRACT_NOT_ACTIVATED u1005`
* citycoin-token: `ERR_TOKEN_NOT_ACTIVATED u2001`

Returns the coinbase thresholds based on the Stacks block height the token was activated, including:

* `coinbaseThreshold1` - the ending block height of the first 210,000 block period, including the 250,000 CityCoin bonus block reward and the 100,000 CityCoin block reward
* `coinbaseThreshold2` - the ending block height of the second  210,000 block period, including the 50,000 CityCoin block reward
* `coinbaseThreshold3` - the ending block height of the third 210,000 block period, including the 25,000 CityCoin block reward
* `coinbaseThreshold4` - the ending block height of the fourth 210,000 block period, including the 12,500 CityCoin block reward
* `coinbaseThreshold5` - the ending block height of the fifth 210,000 block period, including the 6,250 CityCoin block reward

Note: after each threshold is reached above, the perpetual block reward will remain at 3,125 CityCoins per block based on the [emissions schedule](../core-protocol/token-configuration.md#emissions-schedule).

### get-coinbase-amount

Type: Read-only Function

Input: `minerBlockHeight as uint`

Returns: `mintedTokens as uint` based on the [emissions schedule](../core-protocol/token-configuration.md#emissions-schedule) at the given block height

### set-token-uri

Type: Public Function

Input: `newUri as optional string-utf8 256`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`

Updating the token URI ([example: MiamiCoin](https://cdn.citycoins.co/metadata/miamicoin.json)) happens through calling the `set-token-uri` function, which accepts a new URI as an optional parameter.

### send-many

Type: Public Function

Input: `recipients as list of tuples, up to 200, including:`

* `to as principal`
* `amount as uint`
* `memo as optional buff 34`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`

Sending to many recipients happens through calling the `send-many` function in the token contract, which accepts a list up to 200 items in length.

## SIP-010 Functions

[SIP-010](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md) is the standard for fungible tokens on the Stacks blockchain, similar to ERC-20 on Ethereum. As part of the standard, all SIP-010 compliant tokens use the functions defined below.

### transfer

Type: Public Function

Input: `amount as  uint`, `from as principal`, `to as principal`, `memo as  optional buff 34`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`

Transferring CityCoins from one account to another happens through calling the `transfer` function in the token contract, which accepts information about the transfer and an optional memo that is printed on-chain.

### get-name

Type: Read-only Function

Input: `none`

Returns: `(ok tokenName)`

Returns the full name of a CityCoin.

### get-symbol

Type: Read-only Function

Input: `none`

Returns: `(ok tokenSymbol)`

Returns the symbol of a CityCoin.

### get-decimals

Type: Read-only Function

Input: `none`

Returns: `(ok tokenDecimals)`

Returns the number of decimals used for a CityCoin.

### get-balance

Type: Read-only Function

Input: `user as principal`

Returns: `(ok balance)`

Returns the balance for a given user's principal.

### get-total-supply

Type: Read-only Function

Input: `none`

Returns: `(ok totalSupply)`

Returns the total supply for a CityCoin.

_Note: the total supply only increases when miners claim their mining reward._

### get-token-uri

Type: Read-only Function

Input: `none`

Returns: `(ok tokenUri)`

Returns the token URI for a CityCoin.
