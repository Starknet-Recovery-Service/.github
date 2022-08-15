# StarkNet Recovery Service (SRS)

**StarkNet Recovery Service (SRS)** is a fully trustless wallet recovery service for Ethereum L1 EOAs, powered by [storage proofs](https://github.com/OilerNetwork/fossil) on StarkNet. 

Unlike social recovery and other off-chain methods for wallet retrieval, SRS runs in an entirely trustless, non-custodial way. This allows users to build more fault tolerant wallet setups, while retaining the strong security guarantees of Ethereum. 

<img width="2044" alt="image" src="https://user-images.githubusercontent.com/27808560/184609341-70f46a46-4c2c-4bf5-a964-cabab7b59184.png">

<img width="2041" alt="image" src="https://user-images.githubusercontent.com/27808560/184609428-f512d2b7-1c0a-4840-ab86-fcf4467d0880.png">

# How does it work?

To recover user funds, SRS uses [storage proofs](https://github.com/OilerNetwork/fossil) (by Oiler Network) to recursively derive the past state of an EOA and determine whether an account has been lost. This works (broadly) as follows:

1. The owner of an EOA delegates control of their funds to a `RecoveryContract` on L1.
2. Access details for EOA are lost.
3. After a set period of inactivity (say 1 year), the user can call a `StorageProver` contract on StarkNet to verify that the nonce of the lost EOA has not changed over the period. If the test passes, the EOA is treated as lost and the L1 `RecoveryContract` is notified.
4. To recover their assets, the user pings the L1 `RecoveryContract` to withdraw all delegated assets.

SRS is currently deployed for Ethereum L1 but can be ported to any other L1 blockchain which uses Patricia Merkle Trees. 

# Instructions

Users can get started with SRS by interacting with the frontend application deployed at PLACEHOLDER.

Given that this methodology works for any blockchains that uses Patricia merkle trees, developers can build on top of our existing smart contracts or extend them to other Layer 1 blockchains via a cross-chain messaging protocol such as LayerZero. The project files for SRS currently include three repos:

- [`recovery`](https://github.com/StorageProof-Recovery/recovery), which contains the core smart contract logic for consuming storage proofs and handling L1 <> L2 messaging.
- [`recovery-front-end`](https://github.com/StorageProof-Recovery/recovery-front-end), a frontend application for interacting with the deployed smart contracts (using either Argent or Braavos)
- [`recovery-web-hooks`](https://github.com/StorageProof-Recovery/recovery-web-hooks), a server for interacting with and consuming data from the Fossil API.

# Special thanks

[Marcello Bardus](https://github.com/marcellobardus) for building [Fossil](https://github.com/OilerNetwork/fossil) and helping to integrate StarkNet Recovery Service with it. 
