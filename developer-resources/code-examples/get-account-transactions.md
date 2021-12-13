---
description: Getting and manipulating transactions from the Stacks blockchain.
---

# Get Account Transactions

## Getting Account Transactions

The Stacks API [provides an endpoint](https://hirosystems.github.io/stacks-blockchain-api/#operation/get\_account\_transactions) for getting all transactions related to a principal, which can be a Stacks address or a contract identifier.

{% hint style="info" %}
Contract identifiers are formatted _deployer\_address.contract-name_

_e.g._ SP2H8PY27SEZ03MWRKS5XABZYQN17ETGQS3527SA5.newyorkcitycoin-core-v1
{% endhint %}

The `limit` parameter can fetch a maximum of 50 transactions at a time, and the `offset` parameter allows you to set the index for the first transaction to fetch.

Using the `total` value from the initial result, a simple `do...while` loop can help iterate over and collect all transactions for an address.

### Node.js

{% hint style="info" %}
Requires [`node-fetch`](https://www.npmjs.com/package/node-fetch)`in package.json`
{% endhint %}

```
import fetch from "node-fetch";

// returns a Promise that resolves after 'ms' milliseconds
const timer = (ms) => new Promise((res) => setTimeout(res, ms));

// fetches all account transactions for a given address or contract identifier
async function getAccountTxs(address) {
  let counter = 0;
  let total = 0;
  let limit = 50;
  let url = "";
  let txResults = [];

  // bonus points if you use your own node!
  let stxApi = "https://stacks-node-api.mainnet.stacks.co";

  console.log(`checking address: ${address}`);

  // obtain all account transactions 50 at a time
  do {
    url = `${stxApi}/extended/v1/address/${address}/transactions?limit=${limit}&offset=${counter}`;
    const response = await fetch(url);
    if (response.status === 200) {
      // success
      const responseJson = await response.json();
      // get total number of tx
      if (total === 0) {
        total = responseJson.total;
        console.log(`Total Txs: ${total}`);
      }
      // add all transactions to main array
      responseJson.results.map((tx) => {
        txResults.push(tx);
        counter++;
      });
      // output counter
      console.log(`Processed ${counter} of ${total}`);
    } else {
      // error
      throw new Error(
        `getAccountTxs response err: ${response.status} ${response.statusText}`
      );
    }
    // pause for 1sec, avoid rate limiting
    await timer(1000);
  } while (counter < total);

  // view the output
  //console.log(JSON.stringify(txResults));
  
  return txResults;
}

getAccountTxs("SP3CK642B6119EVC6CT550PW5EZZ1AJW661ZMQTYD");

```

## Filtering Transactions

With the full set of transactions for an address, the results can then easily be filtered into a new array with useful data.

### MIA Mining

Filters for all MIA mining transactions for the specified address.

```
// get all MIA mining tx for address
let address = 'SP3CK642B6119EVC6CT550PW5EZZ1AJW661ZMQTYD';
let miningTxs = [];
let txs = getAccountTxs(address);
txs.map(tx => {
  if (tx.tx_type === 'contract_call') {
    if (tx.contract_call.contract_id === `SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.miamicoin-core-v1` && tx.tx_status === 'success') {
      if (tx.contract_call.function_name === 'mine-tokens' || tx.contract_call.function_name === 'mine-many') {
        miningTxs.push(tx);
      }
    }
  }
});

console.log(`total MIA mining txs: ${miningTxs.length}`);
```

### NYC Mining Claims

Filters for all NYC mining claim transactions for the specified address.

```
// get all NYC mining claim tx for address
let miningClaimTxs = [];
let address = 'SP3CK642B6119EVC6CT550PW5EZZ1AJW661ZMQTYD';
let txs = getAccountTxs(address);
txs.map(tx => {
  if (tx.tx_type === 'contract_call') {
    if (tx.contract_call.contract_id === `SP2H8PY27SEZ03MWRKS5XABZYQN17ETGQS3527SA5.newyorkcitycoin-core-v1` && tx.tx_status === 'success') {
      if (tx.contract_call.function_name === 'claim-mining-reward') {
        miningClaimTxs.push(tx);
      }
    }
  }
});
console.log(`total NYC mining claim txs: ${miningClaimTxs.length}`);
```

### MIA Stacking

```
// get all MIA stacking tx for address
let stackingTxs = [];
let address = 'SP3CK642B6119EVC6CT550PW5EZZ1AJW661ZMQTYD';
let txs = getAccountTxs(address);
txs.map(tx => {
  if (tx.tx_type === 'contract_call') {
    if (tx.contract_call.contract_id === `SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.miamicoin-core-v1` && tx.tx_status === 'success') {
      if (tx.contract_call.function_name === 'stack-tokens') {
        stackingTxs.push(tx);
      }
    }
  }
});
console.log(`total MIA stacking txs: ${stackingTxs.length}`);
```

### NYC Stacking Claims

```
// get all NYC stacking claim tx for address
let stackingClaimTxs = [];
let address = 'SP3CK642B6119EVC6CT550PW5EZZ1AJW661ZMQTYD';
let txs = getAccountTxs(address);
txs.map(tx => {
  if (tx.tx_type === 'contract_call') {
    if (tx.contract_call.contract_id === `SP2H8PY27SEZ03MWRKS5XABZYQN17ETGQS3527SA5.newyorkcitycoin-core-v1` && tx.tx_status === 'success') {
      if (tx.contract_call.function_name === 'claim-stacking-reward') {
        stackingClaimTxs.push(tx);
      }
    }
  }
});
console.log(`total NYC stacking claim txs: ${stackingClaimTxs.length}`);
```
