# Launch a Betting parachain 

* ⚡️ Beginner/intermediate
* 👤 Presenter: Alex Bean Casas(Polkadot Support Engineer at Parity)
* 📆 Date scheduled: December 20, 2022 (4PM CET)

👉 [Join the livestream on Twitch](https://www.twitch.tv/polkadotdev) to participate and get your questions answered.

This seminar is based on the workshop presented at the [Metaverse Championships Hackathon](https://metaversechampionship.gg/). Have a look at the [original slide deck](https://docs.google.com/presentation/d/1AYPLyINiBo-G1K_2vN197rUiHWy-UI1h8pDeTOxpIQw/edit#slide=id.g1a972ab7d27_0_0) and the [full pallet code](https://github.com/AlexD10S/substrate-betting) to follow along. The code for the entire parachain node can be found [here](https://github.com/AlexD10S/betting-parachain).

The goal of this seminar is to step developers learning FRAME how to create a custom pallet and integrate it into a parachain node. As stated in the README:

> ⚠️ This is not a production-ready pallet, but a sample built for learning purposes. It is discouraged to use this code 'as-is' in a production runtime.

If you're participating in the seminar, take the opportunity to ask question as we step through the code! You'll have the chance to code along after the seminar.

This seminar will consist of three parts:

1. A walkthrough of the architecture and code of the betting pallet
2. Integrating the betting pallet to a parachain node template
3. Launching the chain and interacting with it

## Architecture

![](https://i.imgur.com/Q7rU7pb.png)

## Pallet code walkthrough

This pallet is inspired by many tutorials in the Ethereum community for making a betting dApp. In a FRAME pallet, there are many similarities, though with pallets we're able to tap into core blockchain functionality such as implementing governance modules, oracles, or clearing storage after betting periods go by. The pallet demonstrated here is kept simple for educational purposes.

**Basics**

1. Configuration trait
2. Events
3. Errors
4. Storage
5. Calls

**More Advanced**

1. Unit tests
2. RPCs ([Tutorial about how to add a custom RPC](https://hackmd.io/JpJCbu0nTa2jym0za1Tggw))
3. Benchmarking 

**Important things to note:**

* 🦀 Storage decisions: easily compare matches using `MatchHashes`.
* 🏦 `MatchDeposit` to create a match to bet and limit of team name sizes and number of bets.
* 🏋️ Benchmarking allows to give the appropriate weights to your pallet's extrinsics.
* 👮‍♂️ For this workshop, `set_result` uses `ensure_root`, i.e. the "sudo" origin which could be a governance origin or trusted oracle. Read more about origins [here](https://docs.substrate.io/build/origins/).

## Integrate pallet into parachain node

In this section we'll integrate our betting pallet into a parachain node using this [node template](https://github.com/substrate-developer-hub/substrate-parachain-template). 

Have a look at the commit [here](https://github.com/AlexD10S/betting-parachain/commit/861096a2263b85a30fb992ac8d887e279c979526#diff-0ec06ea58bd455f09ce6b3bb4c2c1c0d37bda51c1e1be2151c560c9c973959ec) showing how to add the pallet to the parachain node. And have a look [here](https://github.com/AlexD10S/betting-parachain/commit/150d4121362ed6780fd22b40ddc2169de42afae0) at what we need to configure to launch this parachain with Zombienet.

**Important things to note:**
* ✅ A parachain node requires a relay chain node to launch
* 🧟‍♂️ Zombienet is a tool we'll use to launch the parachain + relay chain nodes

## Launching the chain and interacting with it

In this section, we'll launch our parachain and relay chain nodes to interact with the betting pallet.

**Important things to note:**

* 🧟‍♂️ We're launching Zombienet using native binaries. Have a look at Zombienet guides [here](https://paritytech.github.io/zombienet/guide.html).
*  👀 Use the PolkadotJS apps link from launching Zombienet.

## Future

* Create your own front-end using Polkadot JS API
* Create a testing script for Zombienet

## Resources

* Runtime development: https://docs.substrate.io/fundamentals/runtime-development/
* FRAME pallets: https://docs.substrate.io/reference/frame-pallets/
* Origins: https://docs.substrate.io/build/origins/
* Zombienet: https://github.com/paritytech/zombienet
* Parachain node template: https://github.com/substrate-developer-hub/substrate-parachain-template
