---
description: >-
  An overview of the registration and activation component of the CityCoins
  protocol.
---

# Registration and Activation

{% hint style="info" %}
CityCoins require the [Stacks Web Wallet](https://hiro.so/wallet/install-web) to interact with the smart contracts on the [Stacks blockchain](https://stacks.co). (see [How do I get started?](../about-citycoins/how-do-i-get-started.md))
{% endhint %}

CityCoins only exist through mining, which does not begin until 20 independent wallets signal activation after the contract is deployed.

There is no ICO, no pre-sale, and no pre-mine, and there are no CityCoins issued or distributed prior to the start of mining.

Once 20 users register to activate the contract, a 150 block (\~24hr) countdown begins, after which anyone is eligible to try and mine the CityCoins within a given Stacks block.

{% hint style="info" %}
_Registration is not required_ once the contract is activated. After this process is complete, anyone who completes a mining or stacking transaction will automatically be registered as a user.
{% endhint %}

A nominal transaction fee is required in order to send this transaction, paid in STX, and you can optionally include a memo of up to 50 characters that will be recorded on-chain.

For a more technical explanation, please see the [contract functions for activation](../contract-functions/activation.md#overview).
