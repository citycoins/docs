---
description: Implementing and interacting with a Stacks node and related software.
---

# Supporting Stacks

## Overview

In order to efficiently and reliably query the Stacks blockchain state, running a follower node allows for direct access to the same data as hosted APIs with the added benefit of decentralized control.

## Stacks Node API

The Stacks Node API provides both a self-contained Docker image and manual installation instructions for running a Stacks 2.0 blockchain and API instance.

Doing so provides access to a [robust API](https://hirosystems.github.io/stacks-blockchain-api/) that allows for querying accounts, transactions, smart contracts, and more.

* [Main Repository](https://github.com/hirosystems/stacks-blockchain-api)
* [Digital Ocean 1-Click App](https://marketplace.digitalocean.com/apps/stacks-blockchain)
* [Hiro Hosted Version](https://stacks-node-api.testnet.stacks.co/v2/info)
* [API Documentation](https://hirosystems.github.io/stacks-blockchain-api/)

## API Tech Stack

The Stacks Node API can be run on 4 GB memory / 80 GB disk, however it also requires a Bitcoin node to interact with, which have higher [disk space requirements](https://bitcoin.org/en/full-node#minimum-requirements).

The main elements of the API tech stack include:

* Postgres
* Stacks Blockchain API
* Stacks Blockchain Node
* Bitcoin Node

## Updates and Announcements

The [stacks-announce mailing list](https://groups.google.com/a/stacks.org/g/announce) is available to receive updates on new releases to the Stacks blockchain node.

* [Stacks API Releases](https://github.com/hirosystems/stacks-blockchain-api/releases)
* [Stacks Node Releases](https://github.com/blockstack/stacks-blockchain/releases/)

## Installation Methods

{% hint style="info" %}
The [Digital Ocean 1-Click App](https://marketplace.digitalocean.com/apps/stacks-blockchain) is the fastest way to get started, but the options above are available for custom implementations and environments.
{% endhint %}

* [Using Docker](https://github.com/hirosystems/stacks-blockchain-api/blob/master/running\_an\_api.md)
* [Install from Source](https://github.com/hirosystems/stacks-blockchain-api/blob/master/running\_api\_from\_source.md)

The Syvita Guild also created the repository below, which contains a quick start script that sets up each component based on their cloned versions using Docker.

[https://github.com/syvita/stacks-api-node](https://github.com/syvita/stacks-api-node)&#x20;

## Optional: Stacks Explorer

The Stacks Explorer provides a web interface to interact with Stacks blockchain data, including accounts, transactions, contracts, and more.

Some examples include:

* [Hosted by Hiro](https://explorer.stacks.co)
* [Hosted by PlanBetter](https://explorer.planbetter.org/)
* [Hosted by Syvita](https://explorer.syvita.org/)

The Stacks Explorer is [available on GitHub](https://github.com/hirosystems/explorer) built with react, [next.js](https://github.com/zeit/next.js) and [@stacks/ui](https://github.com/blockstack/ui).

## Stacking STX

Stacking is the act of locking up STX for a set number of reward cycles and receiving a portion of the BTC spent by Stacks miners.

We call it "stacking" instead of "staking" because the protocol provides rewards of the _base currency_ instead of the _same currency_.

The Stacking protocol is described in [SIP-007](https://github.com/stacksgov/sips/blob/main/sips/sip-007/sip-007-stacking-consensus.md).

A few high-level notes about the protocol:

* A STX holder must qualify for a reward slot by controlling a Stacks wallet with >= 0.02% of the total unlocked Stacks tokens (currently \~110,000 STX, and visible on [stacking.club](https://stacking.club/))
* A STX holder must broadcast a signed message before the reward cycle begins that:
  * Locks the associated Stacks tokens for a protocol-specified lockup period (reward cycles are 2,100 Stacks blocks in length, maximum of 12)
  * Specifies the Bitcoin address to receive the funds
  * Votes on a Stacks chain tip
* The required minimum for a reward slot is dynamic and can increase last minute. It only increases in steps of 10k STX
* It is possible that a reward slot receives 0 BTC because Stacks miners did not send any BTC when it was the slot's turn
* The more reward slots an address occupies, the closer the payouts will be to the average payout
* When the selected reward cycles are complete, the address must sit out for one cycle (a "cooldown period")

The PoX smart contract is the main tool and provides the functions to stack STX.

It is deployed at [SP000000000000000000002Q6VF78.pox](https://explorer.stacks.co/txid/0x41356e380d164c5233dd9388799a5508aae929ee1a7e6ea0c18f5359ce7b8c33?chain=mainnet).

The documentation is available at [https://docs.blockstack.org/references/stacking-contract](https://docs.blockstack.org/references/stacking-contract).

Additional Stacking information and statistics are available at [https://stacking.club/](https://stacking.club/)
