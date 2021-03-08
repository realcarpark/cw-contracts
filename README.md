# CosmWasm Examples

[![CircleCI](https://circleci.com/gh/CosmWasm/cosmwasm-examples/tree/main.svg?style=shield)](https://circleci.com/gh/CosmWasm/cosmwasm-examples/tree/main)

This repo is a collection of simple contracts built with the
[cosmwasm](https://github.com/CosmWasm/cosmwasm) framework.
Smart contracts here are for only demonstration purposes, **not production ready**.
Production grade smart contracts are collected under [cosmwasm-plus](https://github.com/CosmWasm/cosmwasm-plus).

This repo's organization is relatively simple. The top-level directory is just a placeholder
and has no real code. And we use workspaces to add multiple contracts below.
This allows us to compile all contracts with one command.

## Usage:

The following contracts are available for use. You can view the source code under `src`
and a precompiled wasm ready for deployment under `contract.wasm`. Take a look here:

* [escrow](https://github.com/CosmWasm/cosmwasm-examples/tree/main/escrow) - A basic escrow with timeout and partial release
* [erc20](https://github.com/CosmWasm/cosmwasm-examples/tree/main/erc20) - Basic implementation the erc20 interface for CosmWasm, as a base for token designers

## Development

### Starting a contract

If you want to add a contract, first fork this repo and create a branch for your PR.
I suggest setting it up via [cosmwasm-template](https://github.com/confio/cosmwasm-template):

`cargo generate --git https://github.com/confio/cosmwasm-template.git --name FOO`

Then update the `README.md` to reflect your actual contract (just read the `README.md` in the autogenerated
template - it explains a lot).

### Preparing for merge

Before you merge the code, make sure it builds and passes all tests:

```
./devtools/build_test_all.sh
```

Once you pass these checks, please open a [PR on this repo](https://github.com/CosmWasm/cosmwasm-examples/pulls).

### Release builds

On every tag release builds are automatically created and
[deployed to GitHub Releases](https://github.com/CosmWasm/cosmwasm-examples/releases).

You can build release artifacts manually like this, which creates a reproducible
optimized build for each contract and saves them to the `./artifacts` directory:

```
docker run --rm -v "$(pwd)":/code \
  --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
  cosmwasm/rust-optimizer:0.10.7 ./contracts/*/
```
