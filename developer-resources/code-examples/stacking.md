---
description: Examples of CityCoin contract functions related to stacking.
---

# Stacking

## Stack CityCoins

{% hint style="info" %}
Requires:

* `@stacks/network`
* `@stacks/transactions`
* `@stacks/connect-react`
{% endhint %}

```
// example: stack CityCoins for the next active cycle

const NETWORK = new StacksMainnet(); // set network from @stacks/network
const { doContractCall } = useConnect(); // hook for Stacks Connect

const amount = 250000; // amount of CityCoins
const cycles = 5; // cycles to lock for
const amountCV = uintCV(amount);
const cyclesCV = uintCV(cycles);

try {
  await doContractCall({
    contractAddress: 'SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27',
    contractName: 'miamicoin-core-v1',
    functionName: 'stack-tokens',
    functionArgs: [amountCV, cyclesCV],
    postConditionMode: PostConditionMode.Deny,
    postConditions: [
      makeStandardFungiblePostCondition(
        ownerStxAddress,
        FungibleConditionCode.Equal,
        amountCV.value,
        createAssetInfo('SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27', 'miamicoin-token', 'miamicoin')
      ),
    ],
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
