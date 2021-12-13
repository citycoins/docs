---
description: Examples of CityCoin contract functions related to mining.
---

# Mining

## Mining a Single Block

{% hint style="info" %}
Requires:

* `@stacks/network`
* `@stacks/transactions`
* `@stacks/connect-react`
{% endhint %}

```
// example: mining a single block with 10 STX

const NETWORK = new StacksMainnet(); // set network from @stacks/network
const { doContractCall } = useConnect(); // hook for Stacks Connect

let totalUstx = 10000000; // amount of uSTX to spend in block
let totalUstxCV = uintCV(totalUstx);

let memoCV = someCV(bufferCVFromString('an optional memo'));
// alternate if no memo:
// let memoCV = noneCV();

try {
  await doContractCall({
    contractAddress: 'SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27',
    contractName: 'miamicoin-core-v1',
    functionName: 'mine-tokens',
    functionArgs: [totalUstxCV, memoCV],
    postConditionMode: PostConditionMode.Deny,
    postConditions: [
      makeStandardSTXPostCondition(
        ownerStxAddress,
        FungibleConditionCode.Equal,
        totalUstxCV.value
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

## Mining for Multiple Blocks

{% hint style="info" %}
Requires:

* `@stacks/network`
* `@stacks/transactions`
* `@stacks/connect-react`
{% endhint %}

```
// example: mining 10 blocks with 5, 10, and 15 STX per block

const NETWORK = new StacksMainnet(); // set network from @stacks/network
const { doContractCall } = useConnect(); // hook for Stacks Connect

// initialize variables
let commitsUstx = [5000000, 10000000, 15000000, 5000000, 10000000, 15000000, 5000000, 10000000, 15000000, 5000000];
let totalUstx = 0;
let totalUstxCV = uintCV(0);
let mineManyArray = [];
let mineManyArrayCV = listCV([]);

// set up contract submission data
for (let i = 0; i < commits.length; i++) {
  mineManyArray.push(uintCV(amount));
  totalUstx += amount;
}
totalUstxCV = uintCV(totalUstx);
mineManyArrayCV = listCV(mineManyArray);

try {
  await doContractCall({
    contractAddress: 'SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27',
    contractName: 'miamicoin-core-v1',
    functionName: 'mine-many',
    functionArgs: [mineManyArrayCV],
    postConditionMode: PostConditionMode.Deny,
    postConditions: [
      makeStandardSTXPostCondition(
        ownerStxAddress,
        FungibleConditionCode.Equal,
        totalUstxCV.value
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
