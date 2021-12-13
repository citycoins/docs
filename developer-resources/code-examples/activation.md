---
description: >-
  Examples of CityCoin contract functions related to activation and
  registration.
---

# Activation

## Get Activation Block

Get the block height the contract activates at.

{% hint style="info" %}
Requires `@stacks/network` and `@stacks/transactions`
{% endhint %}

```
// returns the activation block height

const NETWORK = new StacksMainnet(); // set network from @stacks/network

export async function getActivationBlock() {
  const resultCv = await callReadOnlyFunction({
    contractAddress: 'SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27',
    contractName: 'miamicoin-core-v1',
    functionName: 'get-activation-block',
    functionArgs: [],
    network: NETWORK, 
    senderAddress: contractAddress, // can be any valid STX address
  });
  const result = cvToJSON(resultCv);
  return result.value.value; // activation block height
}
```

## Get Registered Users

Get the total number of registered users that have sent one of the following:

* register user tx (`register-user`)
* mining tx (`mine-tokens` or `mine-many`)
* stacking tx (`stack-tokens`)

{% hint style="info" %}
Requires `@stacks/network` and `@stacks/transactions`
{% endhint %}

```
// returns the current number of registered users

const NETWORK = new StacksMainnet(); // set network from @stacks/network

export async function getRegisteredUsersNonce() {
  const resultCv = await callReadOnlyFunction({
    contractAddress: 'SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27',
    contractName: 'miamicoin-core-v1',
    functionName: 'get-registered-users-nonce',
    functionArgs: [],
    network: NETWORK,
    senderAddress: contractAddress, // can be any valid STX address
  });
  const result = cvToJSON(resultCv);
  return result.value; // total registered users
}
```
