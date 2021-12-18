---
description: Creating, monitoring, and interacting with Stacks blockchain transactions.
---

# Stacks Transactions

## Stacks.js Libraries

These libraries include everything you need to work with the [Stacks blockchain](https://stacks.co).

* [Stacks.js Libraries](https://github.com/blockstack/stacks.js)
* [Stacks.js Documentation](https://blockstack.github.io/stacks.js/modules/transactions.html)
* [Stacks.js Documentation (alt)](https://stacks-js-git-master-blockstack.vercel.app)

## Post-Conditions

By defining post conditions, users can create transactions that include pre-defined guarantees about what might happen in that contract.

One such post condition could be "I will transfer exactly 100 of X token", where "X token" is referenced as a specific contract's fungible token. When wallets and applications implement the transfer method, they should always use post conditions to specify that the user will transfer exactly the amount of tokens that they specify in the amount argument of the transfer function. Only in very specific circumstances should such a post condition not be included.

Examples of how to use post-conditions are outlined in the [Code Examples](../code-examples/).

## Fee Estimation

Depending on the number of transactions in the mempool, setting a competitive fee on a transaction can help ensure it's processed in a timely matter by Stacks miners.

Fees are automatically calculated by the [Hiro Web Wallet](https://hiro.so/wallet/install-web) when integrated.
