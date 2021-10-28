# Registration and Activation

## Overview

The launch of a CityCoin happens in a two-step process:

1. The contract for a CityCoin is deployed mainnet on the Stacks blockchain
2. 20 unique wallets send a transaction to the contract signaling activation

Once the threshold is met, a 150 block (\~24hr) countdown begins after which anyone is eligible to mine the CityCoins within a given Stacks block.

There are no CityCoins issued or distributed prior to the start of mining.

## Details

Registration happens by calling the `register-user` function in the CityCoin contract, which can be done with the [Stacks Web Wallet](https://hiro.so/wallet/install-web) through an interface like [minemiamicoin.com](https://minemiamicoin.com).

A nominal transaction fee is required in order to send this transaction, paid in STX, and you can optionally include a memo of up to 50 characters that will be recorded on-chain.

The general process is as follows:

* Download and install the [Stacks Web Wallet](https://hiro.so/wallet/install-web), a browser extension for Chrome/Firefox that interacts with the Stacks blockchain\
  _Note: mobile is not supported at this time, please use a desktop_
* Fund the Stacks address with enough STX to at least cover the transaction fee, or with an amount that you plan to use for mining\
  _Note: to acquire Stacks, please see the _[_market list on CoinMarketCap_](https://coinmarketcap.com/currencies/stacks/markets/)_ for supported exchanges._
* Submit the `register-user` transaction via the user interface, which records your Stacks address and optional memo on chain to signal activation of the CityCoin\
  _Note: once the threshold of 20 miners is reached, mining will begin in 150 Stacks blocks (\~24hrs)_

## Related Contract Functions

### get-activation-block

Type: Read-only Function

Success: `(ok (var-get activationBlock)) returned as a uint`

Error: `ERR_CONTRACT_NOT_ACTIVATED u1005`

Returns the Stacks block height at which the contract was activated, or an error if not.

### get-activation-delay

Type: Read-only Function

Returns: `(var-get activation-delay) as a uint`

Returns the activation delay for mining and Stacking to become available.

### get-activation-status

Type: Read-only Function

Returns: `(var-get activationReached) as a boolean`

Returns the activation status of the contract.

### get-activation-threshold

Type: Read-only Function

Returns: `(var-get activationThreshold) as uint`

Returns the number of users required to register for activation of the contract.

### get-registered-users-nonce

Type: Read-only Function

Returns: `(var-get usersNonce) as uint`

Returns the total number of registered users in the contract, including those registered after activation occurs.

### get-user-id

Type: Read-only Function

Input: `user as principal`

Returns: `(some uint) OR (none)`

Returns the user ID of a given principal.

### get-user

Type: Read-only Function

Input: `userId as uint`

Returns: `(some prinicipal) OR (none)`

Returns the principal of a given user ID.

### register-user

Type: Public Function

Inputs: `optional memo as string-utf8, length 50`

Success: `(ok true)`&#x20;

Errors:

* `ERR_USER_ALREADY_REGISTERED u1001`
* `ERR_ACTIVATION_THRESHOLD_REACHED u1004`

Registration occurs through calling the `register-user` function in the contract, which optionally accepts up to 50 characters as a memo to record on-chain.





``

