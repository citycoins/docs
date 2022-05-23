---
description: CityCoin contract functions related to CityCoin tokens.
---

# Token

## Overview

The CityCoins token contract exists separate from the CityCoins core contract as part of the protocol, however there are some functions used by the core contract to interact with the token.

In addition to those functions, the token contract fully supports the [SIP-010 fungible token standard](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md) on the Stacks blockchain, including functions for [`transfer`](token.md#transfer), [`get-balance`](token.md#get-balance), and more.

CityCoins also support the [`send-many`](token.md#send-many) function, allowing up to 200 transfer operations to be performed in a single transaction.

## Details

{% hint style="info" %}
CityCoins have 6 decimals, denoted with u for micro-.\


1 CityCoin = 1,000,000 micro-CityCoin

1 MIA = 1,000,000 uMIA

1 NYC = 1,000,000 uNYC
{% endhint %}

### Minting

CityCoins can only be minted by a core contract as part of the mining claim process.

CityCoins are not minted until miners claim them.

### Burning

CityCoins can be burned by their owners following the same checks and balances as the transfer function.

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

Returns the coinbase thresholds based on the Stacks block height the token was activated, based on the [emissions schedule](../core-protocol/token-configuration.md#emissions-schedule) as a tuple.

* `coinbaseThreshold1` - bonus + first epoch
* `coinbaseThreshold2` - second epoch
* `coinbaseThreshold3` - third epoch
* `coinbaseThreshold4` - fourth epoch
* `coinbaseThreshold5` - fifth epoch

Note: after each threshold is completed above, the perpetual block reward will remain at 3,125 CityCoins per block based on the sixth epoch in the [emissions schedule](../core-protocol/token-configuration.md#emissions-schedule).

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

### burn

Type: Public Function

Input: `amount as uint` and `owner as principal`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`

Allows a user or contract to burn tokens with the same guards as token transfers.

### convert-to-v2

Type: Public Function

Input: `none`

Success: `(ok true)`

Errors:

* `ERR_V1_BALANCE_NOT_FOUND u2003`

This function checks the V1 CityCoin balance for the user, burns the V1 amount, and mints the equivalent V2 CityCoin amount.

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
