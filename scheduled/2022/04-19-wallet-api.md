## Building decentralized applications with Virto's Wallet API

**Date**: Tuesday, April 19th 2022

**Description:** In this seminar, Daniel Olano lead developer at [Virto.network](http://Virto.nework) will demonstrate the 3 libraries that power what he calls the Wallet API: [Scales](https://github.com/virto-network/scales), [Sube](https://github.com/virto-network/sube) and [Libwallet](https://github.com/virto-network/libwallet). He will talk about his current use cases for these libraries, how he envisions them being used and what it means to build applications that are fully decentralized in the client.


## Plan 
1.  Introduction and about Virto network

3. What is the [Wallet API](https://github.com/virto-network/virto-apis#%EF%B8%8F-wallet-api) 
- What are the different parts of it 
- How does it fit into what you're building
- What makes Sube unique (compared to Subxt for example)

4. High level application design 
- What makes using these tools (Sube, Libwallet and Scales) for building applications different that using Polkadot JS api ? Why can't you just use Polkadot JS API for what you're building?
- What does [progressive decentralization](https://github.com/virto-network/sube#progressive-decentralization) mean to you?

5. Prototype and demo

6. Future
- What are your next steps / future plans
- How can others contribute / get involved

---

### Context

Here's some more context on the original seminar proposal [#7](https://github.com/substrate-developer-hub/substrate-seminar/issues/7).

#### Virto tech stack 

While developing [Virto Network](https://virto.network), the _decentralized infrastructure for marketplaces with social impact_, we have identified a big need to make decentralized applications easier not only to end users but also to developers since the majority are not familiar with concepts unique to Web3 and blockchain and takes time and effort to get onboard.  
Our approach to aid in the Web3 transition is to make use of developer's existing knowledge of the most commonly used technologies, HTTP APIs, virtually every language and platform supports HTTP in one way or another making it the perfect candidate to be the "universal interface" that powers our collection of _decentralizable APIs_. We envision APIs that can be created as simple JS or WASM plugins executed by our runtime _**Valor**_ that runs them in a traditional server environment but also allows said plugins to run in the user's device even(specially) if it is a web browser only application. Developers will have the choice to run APIs in a centralized way in a server, fully decentralized in the client or with a hybrid approach we call _progressive decentralization_.

#### Wallet API
Developers won't have to create all the APIs that power their decentralized application, quite the opposite we want to create an ecosystem of plugins that allow people create a decentralized back-end by picking all the components they need from a catalog in a plug&play manner. The first plugin we are providing to the ecosystem is the **Wallet API** that takes care of the user account, managing keys and all the interactions with the blockchain.

### The talk
Our Wallet API is made from smaller lower level building blocks that are very generic and quite useful on their own. In the talk we'll deep dive into the 3 libraries we created with the help of the Polkadot and Kusama treasuries and talk about the rationale behind their design and how they compare to alternatives already found in the ecosystem.

#### Sube & Scales
[Sube(SUBmit Extrinsics)](https://github.com/virto-network/sube) is lightweight WASM friendly Substrate client with minimal API surface that focuses only on querying a chain's storage & metadata and submitting signed transactions to a Substrate enabled blockchain. It makes use of [Scales(SCALE serialization)](https://github.com/virto-network/scales) that uses the recently added type information to the metadata to be able to convert data to/from human friendly formats like JSON in a dynamic way without having to precompile the types of a specific chain. Sube is also backend agnostic currently using HTTP or WebSockets with planned support for a [smoldot](https://github.com/paritytech/smoldot) based lightclient backend. 

#### [Libwallet](https://github.com/virto-network/libwallet)
An opinionated, again generic, lightweight WASM friendly library for creating chain agnostic wallets. It focuses on abstracting the storage of private keys(the vault) and signing of transactions from multiple sub-accounts that users can create derived from on seed. Portability is a great priority which is why most special functionalities are behind feature flags to not bring unnecessary dependencies(or none at all) to constrained environments like hardware wallets.  
