---
description: Examples of CityCoin contract functions related to mining claims.
---

# Mining Claims

## Claim Mining Rewards

{% hint style="info" %}
Requires:

* `@stacks/network`
* `@stacks/transactions`
* `@stacks/connect-react`
{% endhint %}

```
// example: claim mining rewards at a given block height

const NETWORK = new StacksMainnet(); // set network from @stacks/network
const { doContractCall } = useConnect(); // hook for Stacks Connect

const targetBlock = 24498; // block height to claim
const targetBlockCV = uintCV(targetBlock);

try {
  await doContractCall({
    contractAddress: 'SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27',
    contractName: 'miamicoin-core-v1',
    functionName: 'claim-mining-reward',
    functionArgs: [targetBlockCV],
    postConditionMode: PostConditionMode.Deny,
    postConditions: [],
    network: NETWORK,
    onCancel: () => {
      // what to do if tx is canceled / window is closed
      console.log('Transaction canceled, please try again');
    },
    onFinish: result => {
      // what to if tx is successfully broadcasted
      console.log(`Transaction successfully broadcasted:\n${result.txId}`);
    },
  });
} catch (err) {
  console.log(`Error: ${err.message}`);
}
```

