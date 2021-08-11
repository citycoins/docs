# CityCoin Contracts

## CityCoin

* [citycoin-vrf](https://explorer.stacks.co/txid/0x6e18dbc3a687270a7015ebef73a590d4f066538b41bf7cb7c8d7d891b6442964) single contract used by all cities, takes a given stacks height and returns a uint via the on-chain VRF
* [citycoin-core-trait](https://explorer.stacks.co/txid/0x9751f503896ca13ba797e119d1b62d990b854bee3a63301e737fa9d3ebf8ffa6) single contract used by all cities, defining what a core-v1 contract should have at a minimum
* [citycoin-token-trait](https://explorer.stacks.co/txid/0xf64fedb420622d0403154465c176e06ecbbed306ec2337f9fb8f7bbe6c6a8575) single contract used by all cities, defining what a token contract should have at a minimum

## MiamiCoin

* [miamicoin-core-v1](https://explorer.stacks.co/txid/0x224eb853ab072591c382b1c917136dcdd6590df80ab646bfed432d779612258f?chain=mainnet) contract that enables mining, stacking, and related claims
* [miamicoin-token](https://explorer.stacks.co/txid/0xc513b769c261233865c43f101438bd6359636ecacfe34576e6424d6c2629174e?chain=mainnet) contract that enables sending, send-many, and minting of the token
* [miamicoin-auth](https://explorer.stacks.co/txid/0x3c9303ada7f0dbf6f814722cb4a6c13752f187bde0b800bd6f84a342505e006b?chain=mainnet) contract that enables administrative functions
* [Miami Wallet Address](https://explorer.stacks.co/address/SM2MARAVW6BEJCD13YV2RHGYHQWT7TDDNMNRB1MVT?chain=mainnet) address used by the contract for MiamiCoin protocol distribution

**Please note:** the City of Miami has not yet officially claimed the MiamiCoin protocol contribution.

## Error Codes

### miamicoin-core-v1

| Error Code | Description |
| :--- | :--- |
| u1000 | ERR\_UNAUTHORIZED |
| u1001 | ERR\_USER\_ALREADY\_REGISTERED |
| u1002 | ERR\_USER\_NOT\_FOUND |
| u1003 | ERR\_USER\_ID\_NOT\_FOUND |
| u1004 | ERR\_ACTIVATION\_THRESHOLD\_REACHED |
| u1005 | ERR\_CONTRACT\_NOT\_ACTIVATED |
| u1006 | ERR\_USER\_ALREADY\_MINED |
| u1007 | ERR\_INSUFFICIENT\_COMMITMENT |
| u1008 | ERR\_INSUFFICIENT\_BALANCE |
| u1009 | ERR\_USER\_DID\_NOT\_MINE\_IN\_BLOCK |
| u1010 | ERR\_CLAIMED\_BEFORE\_MATURITY |
| u1011 | ERR\_NO\_MINERS\_AT\_BLOCK |
| u1012 | ERR\_REWARD\_ALREADY\_CLAIMED |
| u1013 | ERR\_MINER\_DID\_NOT\_WIN |
| u1014 | ERR\_NO\_VRF\_SEED\_FOUND |
| u1015 | ERR\_STACKING\_NOT\_AVAILABLE |
| u1016 | ERR\_CANNOT\_STACK |
| u1017 | ERR\_REWARD\_CYCLE\_NOT\_COMPLETED |
| u1018 | ERR\_NOTHING\_TO\_REDEEM |
| ~~_u1019_~~ | ~~_ERR\_UNABLE\_TO\_FIND\_CITY\_WALLET_~~ |
| u1020 | ERR\_CLAIM\_IN\_WRONG\_CONTRACT |

### miamicoin-token

| Error Code | Description |
| :--- | :--- |
| u2000 | ERR\_UNAUTHORIZED |
| u2001 | ERR\_TOKEN\_NOT\_ACTIVATED |
| u2002 | ERR\_TOKEN\_ALREADY\_ACTIVATED |

