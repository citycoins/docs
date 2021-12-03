---
description: CityCoin contract functions related to mining claims.
---

# Mining Claims

### claim-mining-reward

Type: Public Function

Input: `minerBlockHeight as uint`

Success: `(ok true)`

Errors:

* `ERR_USER_NOT_FOUND u1002`
* `ERR_USER_ID_NOT_FOUND u1003`
* `ERR_USER_DID_NOT_MINE_IN_BLOCK u1009`
* `ERR_CLAIMED_BEFORE_MATURITY u1010`
* `ERR_NO_MINERS_AT_BLOCK u1011`
* `ERR_REWARD_ALREADY_CLAIMED u1012`
* `ERR_MINER_DID_NOT_WIN u1013`
* `ERR_NO_VRF_SEED_FOUND u1014`
* `ERR_CLAIM_IN_WRONG_CONTRACT u1020`

Claiming mining rewards happens through calling the `claim-mining-reward` function in the contract, which accepts the block height the miner mined in, and checks if the VRF value is between the `lowValue` and `highValue` for the miner.

If the miner won the block, then the coinbase is minted for them based on block height of the claim and the [issuance schedule](broken-reference).

### is-block-winner

Type: Read-only Function

Input: `user as principal` and `minerBlockHeight as uint`

Returns: `true` or `false`

Returns a boolean value indicating if the user's principal won at a given block height.

_Note: this function will always return false if the token maturity window of 100 blocks did not pass._

### can-claim-mining-reward

Type: Read-only Function

Input: `user as principal` and `minerBlockHeight as uint`

Returns: `true` or `false`

Returns a boolean value indicating if the user's principal won and is eligible to claim the block reward at a given block height.

_Note: this function will always return false if the token maturity window of 100 blocks did not pass._
