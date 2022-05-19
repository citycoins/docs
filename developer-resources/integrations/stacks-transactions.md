---
description: Creating, monitoring, and interacting with Stacks blockchain transactions.
---

# Stacks Transactions

## Stacks.js Libraries

These libraries include everything you need to work with the [Stacks blockchain](https://stacks.co).

* [Stacks.js Libraries](https://github.com/blockstack/stacks.js)
* [Stacks.js Documentation](https://blockstack.github.io/stacks.js/modules/transactions.html)
* [Stacks.js Documentation (alt)](https://stacks-js-git-master-blockstack.vercel.app/)
* [micro-stacks Libraries](https://github.com/fungible-systems/micro-stacks/)
* [micro-stacks Documentation](https://docs.micro-stacks.dev/)

## Post-Conditions

By defining post conditions, users can create transactions that include pre-defined guarantees about what might happen in that contract.

One such post condition could be "I will transfer exactly 100 of X token", where "X token" is referenced as a specific contract's fungible token. When wallets and applications implement the transfer method, they should always use post conditions to specify that the user will transfer exactly the amount of tokens that they specify in the amount argument of the transfer function. Only in very specific circumstances should such a post condition not be included.

```
"post_conditions": [
    {
      "type": "fungible",
      "condition_code": "sent_equal_to",
      "amount": "241996",
      "principal": {
        "type_id": "principal_contract",
        "contract_name": "miamicoin-core-v1",
        "address": "SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27"
      },
      "asset": {
        "contract_name": "miamicoin-token",
        "asset_name": "miamicoin",
        "contract_address": "SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27"
      }
    }
  ],
```

Examples of how to use post-conditions are outlined in the [Code Examples](../code-examples/).

## Fee Estimation

Depending on the number of transactions in the mempool, setting a competitive fee on a transaction can help ensure it's processed in a timely matter by Stacks miners.

Fees are automatically calculated by the [Hiro Web Wallet](https://hiro.so/wallet/install-web) when integrated.

Resources to view the Stacks mempool and more about Stacks transactions are below:

* [Haystack Mempool Explorer](https://haystack.tools/mempool)
* [Stacks data center: mempool](https://stacksdata.info/#mempool)
* [STXStats: transactions per day](https://www.stxstats.co/)
* [CityCoins: get network status script](https://github.com/citycoins/scripts/blob/main/getnetworkstatus.js)
