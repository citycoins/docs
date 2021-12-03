---
description: CityCoin contract functions related to activation and registration.
---

# Activation

### get-activation-block

Type: Read-only Function

Success: `(ok (var-get activationBlock)) returned as a uint`

Error: `ERR_CONTRACT_NOT_ACTIVATED u1005`

Returns the Stacks block height at which the contract was activated, or an error if not.

### get-activation-delay

Type: Read-only Function

Returns: `(var-get activation-delay) as a uint`

Returns the activation delay for mining and Stacking to become available.

### get-activation-status

Type: Read-only Function

Returns: `(var-get activationReached) as a boolean`

Returns the activation status of the contract.

### get-activation-threshold

Type: Read-only Function

Returns: `(var-get activationThreshold) as uint`

Returns the number of users required to register for activation of the contract.

### get-registered-users-nonce

Type: Read-only Function

Returns: `(var-get usersNonce) as uint`

Returns the total number of registered users in the contract, including those registered after activation occurs.

### get-user-id

Type: Read-only Function

Input: `user as principal`

Returns: `(some uint) OR (none)`

Returns the user ID of a given principal.

### get-user

Type: Read-only Function

Input: `userId as uint`

Returns: `(some prinicipal) OR (none)`

Returns the principal of a given user ID.

### register-user

Type: Public Function

Inputs: `optional memo as string-utf8, length 50`

Success: `(ok true)`&#x20;

Errors:

* `ERR_USER_ALREADY_REGISTERED u1001`
* `ERR_ACTIVATION_THRESHOLD_REACHED u1004`

Registration occurs through calling the `register-user` function in the contract, which optionally accepts up to 50 characters as a memo to record on-chain.
