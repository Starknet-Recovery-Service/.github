# Switch (ex. Starknet Recovery Service)

> :warning: Switch is still in development and not ready to be used with live assets. Please proceed with caution.

**Switch** is a fully trustless wallet recovery service for Ethereum Externally Owned Accounts (EOA - your normal Ethereum address, not smart contract wallet), powered by [storage proofs](https://github.com/OilerNetwork/fossil) on StarkNet. 

Unlike social recovery and other off-chain methods for wallet retrieval, Switch runs in an entirely trustless, non-custodial way. This allows users to build more fault tolerant wallet setups, while retaining the strong security guarantees of Ethereum. 

Video presentation + demo: [Link](https://youtu.be/G5FvzoQhGv8)

Slides: [Link](https://app.pitch.com/app/presentation/09ce2e68-01a6-42e2-a195-f5e548aea711/06a878ce-878b-4a1f-9be1-9e125372f4f4/000db933-2625-425b-a1ba-3743a395967f)

![image](https://user-images.githubusercontent.com/27808560/188644772-b4e91247-60ed-4c33-b003-6c763aa893d1.png)

<img width="2041" alt="image" src="https://user-images.githubusercontent.com/27808560/184609428-f512d2b7-1c0a-4840-ab86-fcf4467d0880.png">

# How does it work?

To recover user funds, Switch uses [storage proofs](https://github.com/OilerNetwork/fossil) (by Oiler Network) to recursively derive the past state of an EOA and determine whether an account has been lost. This works (broadly) as follows:

1. The owner of an EOA delegates control of their funds to a `RecoveryContract` on L1.
2. Access details for EOA are lost.
3. After a set period of inactivity (say 1 year), the user can call a `StorageProver` contract on StarkNet to verify that the nonce of the lost EOA has not changed over the period. If the test passes, the EOA is treated as lost and the L1 `RecoveryContract` is notified.
4. To recover their assets, the user pings the L1 `RecoveryContract` to withdraw all delegated assets.

Switch is currently deployed for Ethereum L1 but can be ported to any other L1 blockchain which uses Patricia Merkle Trees. 

# Instructions

Users can get started with Switch by interacting with the frontend application deployed at https://starknet-recovery-service.vercel.app/.

The project files for Switch currently include three repos:

- [`recovery`](https://github.com/StorageProof-Recovery/recovery), which contains the core smart contract logic for consuming storage proofs and handling L1 <> L2 messaging.
- [`recovery-front-end`](https://github.com/StorageProof-Recovery/recovery-front-end), a frontend application for interacting with the deployed smart contracts (using either Argent or Braavos)
- [`recovery-web-hooks`](https://github.com/StorageProof-Recovery/recovery-web-hooks), a server for interacting with and consuming data from the Fossil API.

# Additional Note

Given that this methodology works for any blockchains that uses Patricia merkle trees (such as Solana, Avalanche, Fantom etc.), developers can build on top of our existing smart contracts or extend them to other Layer 1 blockchains via a cross-chain messaging protocol such as LayerZero. 

# Special thanks

[Marcello Bardus](https://github.com/marcellobardus) for building [Fossil](https://github.com/OilerNetwork/fossil) and helping to integrate Switch with it. 
