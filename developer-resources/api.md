---
description: A simple API to interact with Stacks and CityCoins data.
---

# API

The [CityCoins API](https://api.citycoins.co) is a quick and easy way to interact with both Stacks and CityCoins data.

It is built with Cloudflare Workers and micro-stacks, and the [code is open source](https://github.com/citycoins/api).

### Things to Note

* uses simple typed responses and provides detailed error messages
* all CityCoin contract routes start with `:version` and `:cityname`
  * e.g. `/v1/mia/mining/get-mining-stats-at-block/57934`
* `:version` accepts the major CityCoins contract version, e.g. v1, v2
* `:cityname` routes accept three letter city names, e.g. mia, nyc
* all additional parameters follow the order of operations below
  * `:blockheight > :cycleid > :userid > :address`
* routes are structured the same as the contract functions and documentation

### Endpoint Examples

A full list of routes and responses can be found in the [OpenAPI documentation](https://api.citycoins.co/docs).

Some quick examples:

* [Get the current Stacks block height](https://api.citycoins.co/stacks/get-block-height)
* [Get the activation block height for MIA](https://api.citycoins.co/activation/get-activation-block/mia)
* [Get the mining stats at block 49000 for MIA](https://api.citycoins.co/mining/get-mining-stats-at-block/mia/49000)
* [Get the total supply for MIA](https://api.citycoins.co/token/get-total-supply/mia)

### Implementation

If you want to use this for your project, build a copy for yourself, or have any questions, [file a GitHub Issue](https://github.com/citycoins/api/issues/new) and reach out!
