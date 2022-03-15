# Adding new validators to a live test network

Substrate seminar, March 15th 2022.

## Intro 👋 

**Guest:** Ramsey, community member and steward of Kabocha.

**Moderator:** Sacha, developer advocate at Parity.

Recording link: https://www.crowdcast.io/e/substrate-seminar-2/14

## What's Pop-Art and Kabocha? 👀 

Links and resources:
- [Pop-Art intro](https://app.subsocial.network/5779/kabocha-playground-of-possibilities-december-update-27838)
- [Kabocha](https://www.kabocha.network/)

### What we'll be doing 🛠 

_**Note:** This seminar is **not** about connecting your parachain to a relay chain. It assumes you have a test network you want to become a validator for, or that you have one running locally._

Today we'll learn how to **join a test network as a proof of authority validator**, to grow the community of validators on your test networks.

This is generally a good excerice to expose you to how things work when you're launching your own network. 
And starting here will give you good foundations for setting up your own test network.

**Motivation**

- Typically, if you’re building a parachain you’ll need your own test network.
- Why not use an existing one? You can control when it starts and stops and you can access your own validator logs.
- Then, eventually you’ll connect to Rococo, before becoming a parachain on Kusama or Polkadot.

**Why is this important?**

- Getting experience to prepare for the process of connecting a parachain to a testnet.
- You need 2 validators for every parachain connected.

Learning outcomes: makes it clearer what the steps are in preparation for connecting your parachain to a testnet and setting up your own testnet

**Overview for setting up a live testnet:**

1. First set up local testnet (see [this guide](https://docs.substrate.io/tutorials/v3/cumulus/polkadot-launch/)).
2. Second, build a live relay chain and connect multiple validators to it.
3. Then connect a parachain to it.

## Before we begin ✅

We'll be using the terminal to clone, launch and submit RPC calls to our relay chain. 
We'll then use Pokadot JS apps to have a look at our chain's state for things like balances, active nodes and the current validator set.
It helps to be familiar with basic bash and navigating Polkadot JS Apps.

Useful tutorials:

- [Start a permissioned network](https://docs.substrate.io/tutorials/v3/permissioned-network/)
- [Start a private network](https://docs.substrate.io/tutorials/v3/private-network/)

## Let's get started 🌟 

**Steps:**

1. Compile the [Pop-art relay chain](https://github.com/kabocha-network/relay-chain)
    
    `git clone -b v0.9.16-n1 https://github.com/kabocha-network/relay-chain.git`
    
    `cd relay-chain && cargo build --release`    
    
2. Launch an instance of this node, and verify that its peering with the other nodes of the network.

```bash
./target/release/polkadot \
--validator \
--base-path /usr/local/bin/polkadot \
--unsafe-ws-external \
--rpc-methods=Unsafe \
--rpc-external=True \
--rpc-cors all \
--port 30333 \
--ws-port 9944 \
--rpc-port 9933 \
--chain ./specs/pop-art-3-val.json \
--telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \
--name SachaNode01 \
```

Our chain spec already contains bootnodes, but if you come across a chain spec without any bootnodes, ask a comrade who is running a node to provide you with a bootnode address and then add the `--bootnodes` flag to your command with that address.

**Tip💡**: if you wanted to launch another node from the same machine, you can accelerate the synching by copying the files in your chain's `db` to a new base path. First:
`mkdir /usr/local/bin/polkadot2/chains/rococo_staging_testnet/db/full/`

then:

`cp -r /usr/local/bin/polkadot/chains/rococo_staging_testnet/db/full/ /usr/local/bin/polkadot2/chains/rococo_staging_testnet/db/full/`

3. You should see your node synching with the other peers in the network by going to [Polkadot JS Apps](https://apps.decentration.org/?rpc=wss%3A%2F%2Fpopart1.jelliedowl.com#/explorer/node).

You'll notice your node is just an Authority node but we're yet to add it to the validator set.

4. Generate your node's private and public keys for BABE and GRANDPA. These are hot keys, just for test networks:

For BABE:

`subkey generate --scheme SR25519`

For GRANDPA:

`subkey generate --scheme ED25519`

Save these in a text editor somewhere.

5. Submit an RPC call using your BABE keypair:

```bash
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", 
"method": "author_insertKey", "params":["babe", "best squeeze they prefer attract fix arrest busy olympic glimpse cable raccoon", "0xe0625d45afa966320e2328294e71d9d59fc1e18c0ab2a1623c86be943e6d4217"] }' http://127.0.0.1:9933
```

_The result should return `{"jsonrpc":"2.0","result":null,"id":1}`._

6. Submit an RPC call using your GRANDPA keypair:

```bash
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", 
"method": "author_insertKey", "params":["babe", "awake leg drop eyebrow ensure used patrol service pride gown citizen machine", "0xf4c3f7d6b068c18733548cae3cbba549793f850bce73f126096d81b830969a16"] }' http://127.0.0.1:9933
```

_The result should return `{"jsonrpc":"2.0","result":null,"id":1}`._

7. Submit another RPC call to generate new session keys using [`author_rotateKeys`](https://docs.substrate.io/rustdocs/latest/sc_rpc/author/trait.AuthorApi.html#tymethod.rotate_keys). Make sure to input the correct port! 

```bash=
curl -H 'Content-Type: application/json' --data '{ “jsonrpc”:”2.0", "method":"author_rotateKeys", "id":1 }' http://127.0.0.1:9933
```

The result should return: `{"jsonrpc":"2.0","result":null, "id":null}` followed by a hex-encoded blob in the result field, which is the concatenation of the four public keys.

If this step worked correctly, you’ll see it in your keystore. For example, in: `/usr/local/bin/polkadot/chains/rococo_staging_testnet/keystore`

8. Request network tokens from a network admin or a comrade who holds some.

9. Set your session keys.

You need to tell the chain what your Session keys are by submitting an extrinsic. This will associate your validator node with your account.

Go to `Polkadot JS Apps -> Developer -> Extrinsics -> session -> setKeys`. 

In the `keys` field, paste in the result from (7).

In the proof field, just put `0x00`.

10. Add your key as a validator by submitting a `ValidationManager -> registerValidators` extrinsic.

11. You should see your node become a validator in Polkadot JS apps by looking at the validator set.

12. Connect to [Telemetry](https://telemetry.polkadot.io/#/0xd693b58399f3666610f7fbd9d5fad9ad7ec24de1229a2cb0be6d47f8e1c17f41) to check that your node appears. In the next epoch, it will be included in the validator set.

## Questions, review and common errors 🤔

A couple things to go over:

- What's being stored locally ?
    - Base path folder
- How can I ensure my validator stays active? 
    - Digital Ocean Droplet 
- Common errors and issues
    - Not all nodes peer with other nodes: synching all the blocks
- Where does the chainspec come from?
    - How can I verify it's correct?
- How does the sudo account for the network get set?
    - What would the steps be for making some governance orgin instead?
- What's the difference between a validator and a synching node?
- How to clear local chain data?
    - `./target/release/polkadot purge-chain`
- What are the costs for running your own testnet validator? 
- What's next? 
    - Connect a parachain to a relay network
    - Create your own relay network

## Resources 📚
- [How to connect your parachain to Rococo](https://docs.substrate.io/tutorials/v3/cumulus/rococo/) (Substrate docs)
- [How to add new validators to your testnet](https://decentration.medium.com/set-up-public-relay-validators-with-a-partner-3ef409c675c7) (Medium article by Decentration)
- [Different types of nodes](https://wiki.polkadot.network/docs/maintain-sync#types-of-nodes) (Polkadot wiki)
- [Being a validator on Polkadot](https://wiki.polkadot.network/docs/maintain-index#validator) (Polkadot wiki)
- [Session keys](https://docs.substrate.io/v3/concepts/session-keys/) (Substrate docs)
