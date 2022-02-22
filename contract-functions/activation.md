---
description: CityCoin contract functions related to activation and registration.
---

# Activation

## Overview

The launch of a CityCoin happens in a two-step process:

1. The contract for a CityCoin is deployed mainnet on the Stacks blockchain
2. 20 unique wallets send a transaction to the contract signaling activation

Once the threshold is met, a 150 block (\~24hr) countdown begins after which anyone is eligible to try and mine the CityCoins within a given Stacks block.

There are no CityCoins issued or distributed prior to the start of mining.

## Details

Registration happens by calling the [`register-user`](activation.md#register-user) function in the CityCoin contract, which can be done with the [Stacks Web Wallet](https://hiro.so/wallet/install-web) through an interface like [minecitycoins.com](https://minecitycoins.com).

{% hint style="info" %}
An example of the code used in the CityCoins UI can be found in the [RegisterUser component](https://github.com/citycoins/citycoin-ui/blob/main/src/components/activation/RegisterUser.js) on GitHub.
{% endhint %}

A nominal transaction fee is required in order to send this transaction, paid in STX, and you can optionally include a memo of up to 50 characters that will be recorded on-chain.

Once the threshold is reached, the `register-user` function will:

* calculate the activation block height + the activation delay
* set the `core` as active in the core contract map in `auth`
*   set the `token` as active and set the coinbase thresholds

    (based on the activation block height)
* set the coinbase thresholds in `core` to match that of `token`

## Functions

### [API Ref: Activation](https://api.citycoins.co/docs#tag/Activation)

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

Returns: `(some principal) OR (none)`

Returns the principal of a given user ID.

### register-user

Type: Public Function

Inputs: `optional memo as string-utf8, length 50`

Success: `(ok true)`&#x20;

Errors:

* `ERR_USER_ALREADY_REGISTERED u1001`
* `ERR_ACTIVATION_THRESHOLD_REACHED u1004`

Registration occurs through calling the `register-user` function in the contract, which optionally accepts up to 50 characters as a memo to record on-chain.
