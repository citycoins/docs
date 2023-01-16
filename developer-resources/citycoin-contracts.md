---
description: Links and information about deployed CityCoin contracts.
---

# Contracts

## CityCoins Protocol

Content will be added here following the mainnet deployments of the protocol outlined in [CCIP-013](https://github.com/citycoins/governance/blob/main/ccips/ccip-013/ccip-013-stabilize-protocol-and-simplify-contracts.md).

## CityCoins Testnet Protocol

In order to facilitate testing of the legacy CityCoins protocol migration to the new structure outlined in [CCIP-013](https://github.com/citycoins/governance/blob/main/ccips/ccip-013/ccip-013-stabilize-protocol-and-simplify-contracts.md), the legacy CityCoins protocol is now deployed to testnet and activated for mining and stacking.

If you need testnet STX, MIA, or NYC for testing, reach out in the `#path-forward` channel on [Discord](https://chat.citycoins.co).

### CityCoins DAO Structure

The CityCoins DAO implementation is based on the [Executor DAO](https://github.com/MarvinJanssen/executor-dao), [Ecosystem DAO](https://stx.eco/), and other similar implementations on the Stacks blockchain.

The core concepts that make this possible are:

* proposals are smart contracts that execute the described changes
* the core (base-dao) executes proposals, the extensions define additional actions
* ownership control happens via sending context

### CityCoins DAO Extensions

In order to achieve the structure and goals laid out by CCIP-013, the following DAO extensions provide functionality for each part of the CityCoins protocol.

| Name                   | Summary                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                                                                   |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ccd001-direct-execute  | Allows a small number of very trusted principals to immediately execute a proposal once a super majority is reached. | An extension meant for the bootstrapping period of a DAO. It temporarily gives trusted principals the ability to perform a "direct execution"; meaning, they can immediately execute a proposal with the required signals. The Direct Execute extension is set with a sunset period of \~6 months from deployment. Approvers, the parameters, and sunset period may be changed by means of a future proposal. |
| ccd002-treasury        | A treasury contract that can manage STX, SIP-009 NFTs, and SIP-010 FTs.                                              | An extension contract that holds assets on behalf of the DAO. SIP-009 and SIP-010 assets must be allowed before they are supported. Deposits can be made by anyone either by transferring to the contract or using a deposit function below. Withdrawals are restricted to the DAO through either extensions or proposals.                                                                                    |
| ccd003-user-registry   | A central user registry for the CityCoins protocol.                                                                  | An extension contract that associates an address (principal) with an ID (uint) for use in other CityCoins extensions.                                                                                                                                                                                                                                                                                         |
| ccd004-city-registry   | A central city registry for the CityCoins protocol.                                                                  | An extension contract that associates a city name (string-ascii 10) with an ID (uint) for use in other CityCoins extensions.                                                                                                                                                                                                                                                                                  |
| ccd005-city-data       | A datastore for city information in the CityCoins protocol.                                                          | An extension contract that uses the city ID as the key for storing city information. This contract is used by other CityCoins extensions to store and retrieve city information.                                                                                                                                                                                                                              |
| ccd006-city-mining     | A central city mining contract for the CityCoins protocol.                                                           | An extension that provides a mining interface per city, in which each mining participant spends STX per block for a weighted chance to mint new CityCoins per the issuance schedule.                                                                                                                                                                                                                          |
| ccd007-city-stacking   | A central city stacking contract for the CityCoins protocol.                                                         | An extension that provides a stacking interface per city, in which a user can lock their CityCoins for a specified number of cycles, in return for a proportion of the stacking rewards accrued by the related city wallet.                                                                                                                                                                                   |
| ccd008-city-activation | This extension allows anyone to vote on activating a city once it's been added to CCD005 City Data.                  | An extension contract that handles the voting process for activating a city and setting the related data.                                                                                                                                                                                                                                                                                                     |
| ccd009-auth-v2-adapter | Connects to the auth v2 contract in the CityCoins protocol as an approver.                                           | This allows the DAO to access protected contract functions in the old protocol as part of CCIP-010.                                                                                                                                                                                                                                                                                                           |

### Deployer Addresses

| Deployer Type | Mainnet Address                                                                                                                                | Testnet Address                                                                                                                                |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| MIA           | SP1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8Y634C7R [(link)](https://explorer.stacks.co/address/SP1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8Y634C7R?chain=mainnet) | ST1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8WRH7C6H [(link)](https://explorer.stacks.co/address/ST1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8WRH7C6H?chain=testnet) |
| NYC           | SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11 [(link)](https://explorer.stacks.co/address/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11?chain=mainnet)   | STSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1D64KKHQ [(link)](https://explorer.stacks.co/address/STSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1D64KKHQ?chain=testnet)   |
| DAO           | SP355N8734E5PVX9538H2QGMFP38RE211D9KV4MW8 [(link)](https://explorer.stacks.co/address/SP355N8734E5PVX9538H2QGMFP38RE211D9KV4MW8?chain=mainnet) | ST355N8734E5PVX9538H2QGMFP38RE211D9E2B4X5 [(link)](https://explorer.stacks.co/address/ST355N8734E5PVX9538H2QGMFP38RE211D9E2B4X5?chain=testnet) |
| Traits        | SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11 [(link)](https://explorer.stacks.co/address/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11?chain=mainnet)   | ST3AY0CM7SD9183QZ4Y7S2RGBZX9GQT54MJ6XY0BN [(link)](https://explorer.stacks.co/address/ST3AY0CM7SD9183QZ4Y7S2RGBZX9GQT54MJ6XY0BN?chain=testnet) |

{% hint style="info" %}
The accounts for MIA, NYC, and the DAO deployments are the same for mainnet and testnet, with each address version linked above.\
\
The traits for the MIA/NYC protocol were deployed to `SPSCW...DYQ11` on mainnet and the separate account/address `ST3AY...XY0BN` on testnet.\
\
The traits for the CityCoins DAO will be deployed on mainnet by the same deployer as the DAO: `SP355...V4MW8`.
{% endhint %}

### Testnet Approvers

To facilitate faster testing, the list of approvers for the DAO's ccd001-direct-execute module all come from the same account and are noted below. On mainnet this will be a distributed group of signers.

* [`ST3AY0CM7SD9183QZ4Y7S2RGBZX9GQT54MJ6XY0BN`](https://explorer.stacks.co/address/ST3AY0CM7SD9183QZ4Y7S2RGBZX9GQT54MJ6XY0BN?chain=testnet)
* [`ST2D06VFWWTNCWHVB2FJ9KJ3EB30HFRTHB1A4BSP3`](https://explorer.stacks.co/address/ST2D06VFWWTNCWHVB2FJ9KJ3EB30HFRTHB1A4BSP3?chain=testnet)
* [`ST113N3MMPZRMJJRZH6JTHA5CB7TBZH1EH4C22GFV`](https://explorer.stacks.co/address/ST113N3MMPZRMJJRZH6JTHA5CB7TBZH1EH4C22GFV?chain=testnet)
* [`ST8YRW1THF2XT8E45XXCGYKZH2B70HYH71VC7737`](https://explorer.stacks.co/address/ST8YRW1THF2XT8E45XXCGYKZH2B70HYH71VC7737?chain=testnet)
* [`STX13Q7ZJDSFVDZMQ1PWDFGT4QSBMASRMCYE4NAP`](https://explorer.stacks.co/address/STX13Q7ZJDSFVDZMQ1PWDFGT4QSBMASRMCYE4NAP?chain=testnet)

### Testnet City Wallets

The following accounts represent the city wallet in the legacy version of the protocol on testnet, which will be retired in favor of the ccd002-treasury equivalents.

* MIA: [`ST3PM583Q21NF0GB428P79VFPYH8X5DQVKDDGD74T`](https://explorer.stacks.co/address/ST3PM583Q21NF0GB428P79VFPYH8X5DQVKDDGD74T?chain=testnet)
* NYC: [`ST7G6VDV48CXXSP6J2B4RRCKTFJ5NK3PBZSD3YW5`](https://explorer.stacks.co/address/ST7G6VDV48CXXSP6J2B4RRCKTFJ5NK3PBZSD3YW5?chain=testnet)

### Legacy Protocol

The following contracts are deployed on testnet for the legacy CityCoins protocol.

| MIA                                                                                                                              | NYC                                                                                                                                         |
| -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| [miamicoin-auth-v2](https://explorer.stacks.co/txid/ST1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8WRH7C6H.miamicoin-auth-v2?chain=testnet)   | [newyorkcitycoin-auth-v2](https://explorer.stacks.co/txid/STSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1D64KKHQ.newyorkcitycoin-auth-v2?chain=testnet)   |
| [miamicoin-core-v2](https://explorer.stacks.co/txid/ST1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8WRH7C6H.miamicoin-core-v2?chain=testnet)   | [newyorkcitycoin-core-v2](https://explorer.stacks.co/txid/STSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1D64KKHQ.newyorkcitycoin-core-v2?chain=testnet)   |
| [miamicoin-token-v2](https://explorer.stacks.co/txid/ST1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8WRH7C6H.miamicoin-token-v2?chain=testnet) | [newyorkcitycoin-token-v2](https://explorer.stacks.co/txid/STSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1D64KKHQ.newyorkcitycoin-token-v2?chain=testnet) |

These contracts will be migrated to the CityCoins DAO protocol per CCIP-013 on testnet first.

## CityCoins (Legacy Info)

|                                                                                                                                        V1                                                                                                                                       |                                                                                                                                           V2                                                                                                                                          |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|           <p><a href="https://explorer.stacks.co/txid/SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.citycoin-vrf?chain=mainnet">citycoin-vrf</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-006/ccip-006-citycoins-vrf.md">CCIP-006</a>)</p>          |         <p><a href="https://explorer.stacks.co/txid/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11.citycoin-vrf-v2?chain=mainnet">citycoin-vrf-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-009/ccip-009-citycoins-vrf-v2.md">CCIP-009</a>)</p>         |
|  <p><a href="https://explorer.stacks.co/txid/SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.citycoin-core-trait?chain=mainnet">citycoin-core-trait</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-001/ccip-001-citycoins-traits.md">CCIP-001</a>)</p>  |  <p><a href="https://explorer.stacks.co/txid/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11.citycoin-core-v2-trait?chain=mainnet">citycoin-core-v2-trait</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-001/ccip-001-citycoins-traits.md">CCIP-001</a>)</p>  |
| <p><a href="https://explorer.stacks.co/txid/SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.citycoin-token-trait?chain=mainnet">citycoin-token-trait</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-001/ccip-001-citycoins-traits.md">CCIP-001</a>)</p> | <p><a href="https://explorer.stacks.co/txid/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11.citycoin-token-v2-trait?chain=mainnet">citycoin-token-v2-trait</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-001/ccip-001-citycoins-traits.md">CCIP-001</a>)</p> |

The VRF is a single contract used by all mining contracts, which takes a given Stacks block height and returns a random `uint` calculated by accessing the on-chain VRF.

* V1: includes a read-only function that calculates the value and returns it
* V2: includes a public function that will set the value to a map before returning it, and both the public and read-only function check the map for a value before calculating it

The core trait defines the functions in a `citycoin-core-*` contract around activation, mining, and stacking.

The token trait defines the functions in a `citycoin-token-*` contract around token utilities and a send-many function.

{% hint style="warning" %}
Clarity traits allow creating generalized functions where the contract to use within the function is provided as a parameter. This requires [extra security considerations](https://github.com/LNow/clarity-notes/blob/main/security/traits.md).
{% endhint %}

### MiamiCoin (MIA)

|                                                                                                                                                                                                                                                              V1                                                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                              V2                                                                                                                                                                                                                                                              |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                                                                                                                              <p><a href="https://explorer.stacks.co/txid/SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.miamicoin-auth?chain=mainnet">miamicoin-auth</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-007/ccip-007-citycoins-auth.md">CCIP-007</a>)</p>                                                                                                                              |                                                                                                                          <p><a href="https://explorer.stacks.co/txid/SP1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8Y634C7R.miamicoin-auth-v2?chain=mainnet">miamicoin-auth-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-010/ccip-010-citycoins-auth-v2.md">CCIP-010</a>)</p>                                                                                                                         |
| <p><a href="https://explorer.stacks.co/txid/SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.miamicoin-core-v1?chain=mainnet">miamicoin-core-v1</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-002/ccip-002-citycoins-activation.md">CCIP-002</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-003/ccip-003-citycoins-mining.md">CCIP-003</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-004/ccip-004-citycoins-stacking.md">CCIP-004</a>)</p> | <p><a href="https://explorer.stacks.co/txid/SP1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8Y634C7R.miamicoin-core-v2?chain=mainnet">miamicoin-core-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-002/ccip-002-citycoins-activation.md">CCIP-002</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-003/ccip-003-citycoins-mining.md">CCIP-003</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-004/ccip-004-citycoins-stacking.md">CCIP-004</a>)</p> |
|                                                                                                                         <p><a href="https://explorer.stacks.co/txid/SP466FNC0P7JWTNM2R9T199QRZN1MYEDTAR0KP27.miamicoin-token?chain=mainnet">miamicoin-token</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-005/ccip-005-citycoins-sip-010-token.md">CCIP-005</a>)</p>                                                                                                                        |                                                                                                                    <p><a href="https://explorer.stacks.co/txid/SP1H1733V5MZ3SZ9XRW9FKYGEZT0JDGEB8Y634C7R.miamicoin-token-v2?chain=mainnet">miamicoin-token-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-008/ccip-008-citycoins-sip-010-token-v2.md">CCIP-008</a>)</p>                                                                                                                    |

The auth, core, and token contract are created to interact with each other such that:

* The `core` contract enables activation/mining/stacking
* The `token` contract enables the CityCoin token operations
* The `auth` contract enables administrative utilities

The [Miami Wallet Address](https://explorer.stacks.co/address/SM2MARAVW6BEJCD13YV2RHGYHQWT7TDDNMNRB1MVT?chain=mainnet) is used by the contract for MiamiCoin protocol distribution.

### NewYorkCityCoin (NYC)

|                                                                                                                                                                                                                                                                    V1                                                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                    V2                                                                                                                                                                                                                                                                   |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                                                                                                                              <p><a href="https://explorer.stacks.co/txid/SP2H8PY27SEZ03MWRKS5XABZYQN17ETGQS3527SA5.newyorkcitycoin-auth?chain=mainnet">newyorkcitycoin-auth</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-007/ccip-007-citycoins-auth.md">CCIP-007</a>)</p>                                                                                                                              |                                                                                                                          <p><a href="https://explorer.stacks.co/txid/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11.newyorkcitycoin-auth-v2?chain=mainnet">newyorkcitycoin-auth-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-010/ccip-010-citycoins-auth-v2.md">CCIP-010</a>)</p>                                                                                                                         |
| <p><a href="https://explorer.stacks.co/txid/SP2H8PY27SEZ03MWRKS5XABZYQN17ETGQS3527SA5.newyorkcitycoin-core-v1?chain=mainnet">newyorkcitycoin-core-v1</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-002/ccip-002-citycoins-activation.md">CCIP-002</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-003/ccip-003-citycoins-mining.md">CCIP-003</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-004/ccip-004-citycoins-stacking.md">CCIP-004</a>)</p> | <p><a href="https://explorer.stacks.co/txid/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11.newyorkcitycoin-core-v2?chain=mainnet">newyorkcitycoin-core-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-002/ccip-002-citycoins-activation.md">CCIP-002</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-003/ccip-003-citycoins-mining.md">CCIP-003</a>, <a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-004/ccip-004-citycoins-stacking.md">CCIP-004</a>)</p> |
|                                                                                                                         <p><a href="https://explorer.stacks.co/txid/SP2H8PY27SEZ03MWRKS5XABZYQN17ETGQS3527SA5.newyorkcitycoin-token?chain=mainnet">newyorkcitycoin-token</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-005/ccip-005-citycoins-sip-010-token.md">CCIP-005</a>)</p>                                                                                                                        |                                                                                                                    <p><a href="https://explorer.stacks.co/txid/SPSCWDV3RKV5ZRN1FQD84YE1NQFEDJ9R1F4DYQ11.newyorkcitycoin-token-v2?chain=mainnet">newyorkcitycoin-token-v2</a><br>(<a href="https://github.com/citycoins/governance/blob/main/ccips/ccip-008/ccip-008-citycoins-sip-010-token-v2.md">CCIP-008</a>)</p>                                                                                                                    |

The auth, core, and token contract are created to interact with each other such that:

* The `core` contract enables activation/mining/stacking
* The `token` contract enables the CityCoin token operations
* The `auth` contract enables administrative utilities

The [New York City Wallet Address](https://explorer.stacks.co/address/SM18VBF2QYAAHN57Q28E2HSM15F6078JZYZ2FQBCX?chain=mainnet) is used by the contract for NewYorkCityCoin protocol distribution.
