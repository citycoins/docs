---
description: >-
  An overview of the registration and activation component of the CityCoins
  protocol.
---

# Registration and Activation

## Overview

The launch of a CityCoin happens in a two-step process:

1. The contract for a CityCoin is deployed mainnet on the Stacks blockchain
2. 20 unique wallets send a transaction to the contract signaling activation

Once the threshold is met, a 150 block (\~24hr) countdown begins after which anyone is eligible to mine the CityCoins within a given Stacks block.

There are no CityCoins issued or distributed prior to the start of mining.

## Details

Registration happens by calling the `register-user` function in the CityCoin contract, which can be done with the [Stacks Web Wallet](https://hiro.so/wallet/install-web) through an interface like [minecitycoins.com](https://minecitycoins.com).

A nominal transaction fee is required in order to send this transaction, paid in STX, and you can optionally include a memo of up to 50 characters that will be recorded on-chain.

The general process is as follows:

* Download and install the [Stacks Web Wallet](https://hiro.so/wallet/install-web), a browser extension for Chrome/Firefox that interacts with the Stacks blockchain\
  _Note: mobile is not supported at this time, please use a desktop_
* Fund the Stacks address with enough STX to at least cover the transaction fee, or with an amount that you plan to use for mining\
  _Note: to acquire Stacks, please see the_ [_market list on CoinMarketCap_](https://coinmarketcap.com/currencies/stacks/markets/) _for supported exchanges._
* Submit the `register-user` transaction via the user interface, which records your Stacks address and optional memo on chain to signal activation of the CityCoin\
  _Note: once the threshold of 20 miners is reached, mining will begin in 150 Stacks blocks (\~24hrs)_
