# Token Configuration

## Overview

The token exists separate from the core contract as part of the CityCoins Token Protocol, however there are some functions used by the core contract to interact with the token.

In addition to those functions, the token contract fully supports the SIP-010 fungible token standard on the Stacks blockchain.

## Related Contract Functions

### activate-token

Type: Public Function

Input: `coreContract as principal` and `stacksHeight as uint`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`
* `ERR_TOKEN_ALREADY_ACTIVATED u2002`

A one-time use function to activate the token halving as defined in the [issuance schedule](issuance-schedule.md) at a given Stacks block height. This function must be called by an active core contract, and once called, cannot be used again.

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

Note: after each threshold is reached above, the perpetual block reward will remain at 3,125 CityCoins per block based on the [issuance schedule](issuance-schedule.md).

### get-coinbase-amount

Type: Read-only Function

Input: `minerBlockHeight as uint`

Returns: `mintedTokens as uint` based on the [issuance schedule](issuance-schedule.md) at the given block height

### set-token-uri

Type: Public Function

Input: `newUri as optional string-utf8 256`

Success: `(ok true)`

Errors:

* `ERR_UNAUTHORIZED u2000`

Updating the token URI \([example: MiamiCoin](https://cdn.citycoins.co/metadata/miamicoin.json)\) happens through calling the `set-token-uri` function, which accepts a new URI as an optional parameter.

### send-many

Type: Public Function



## SIP-010 Functions

### transfer

Type: Public Function

### get-name

Type: Read-only Function

### get-symbol

Type: Read-only Function

### get-decimals

Type: Read-only Function

### get-balance

Type: Read-only Function

### get-total-supply

Type: Read-only Function

### get-token-uri

Type: Read-only Function



