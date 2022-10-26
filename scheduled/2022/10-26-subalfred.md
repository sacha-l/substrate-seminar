## SubAlfred: the all-in-one Substrate developer toolbox

* ⚡️ Beginner / intermediate
* 👤 Presenter: Xavier
* 📆 Date scheduled: October 26, 2022

👉 [Join the livestream on Crowdcast](https://www.crowdcast.io/e/substrate-seminar-2/26).

### Description

Learn how you can use SubAlfred's key utilities, whether you're a parachain developer or just getting started with Substrate.
SubAlfred provides parachain developers with a bunch of utilities for working with Substrate and testing runtime upgrades.

Some ideas that were initially proposed for this seminar's presenter to cover were:
* Runtime upgrades and how to _dry-run_ runtime upgrades
* Forking live chains/rewriting a chainspec with alice keys
* Querying for pallet prefixes

### Topic

Tools, Runtime migrations, Substrate utils

### Plan

The plan is to go over each command with real-world examples of usage.

The commands include:
* `check`
* `convert`
* `get`
* `hash`
* `key`
* `state`
* `storage-key`
* `workspace`

Xavier will go through this list, with a focus on using `check` in a project's CI and how to use `state` on a template chain.

### Links and resources

* [SubAlfred documentation](https://subalfred.hack.ink/)
* [SubAlfred Github](https://github.com/hack-ink/subalfred)

-----------

_(pasted from Xavier's write-up)_

## About me (Xavier)

- I'm active on the [stackexchange](https://substrate.stackexchange.com/users/251/aurevoirxavier).
- I love helping people to solve their questions.
- I'm a core developer from @darwinia-network.
- I have worked for the Substrate/Polkadot ecosystem since 2019.
- I'm also the author of [array-bytes](https://github.com/hack-ink/array-bytes) and [subalfred](https://github.com/hack-ink/subalfred).

## What's Subalfred?
The goal of Subalfred is to be an all-in-one Substrate development toolbox.

By the end of this seminar, you will have learnt how to use this tool to speed up the Substrate development process.

# Follow along

## [Installing](https://subalfred.hack.ink/user/installation.html)

## Commands

How to query the `Polkadot::System::Account(Gavin)` in terminal?

Known:
```
gavin       = 13RDY9nrJpyTDBSUdBw12dGwhk19sGwsrVZ2bxkzYHBSagP2
storage key = twox128(System) + twox128(Account) + blake2-128-concat(public key)
```

### [storage-key command](https://subalfred.hack.ink/user/cli/storage-key.html)
The first thing we need to know is the storage key of pallet prefix and the storage item prefix.

We just need to run:
```
subalfred storage-key --prefix System --item Account
```
Then we got the result:
```
0x26aa394eea5630e07c48ae0c9558cef7b99d880ec681799c0cf30e8886371da9
```

Let's check if the result is the same as the PolkadotApps' one.

### [key command](https://subalfred.hack.ink/user/cli/key.html)
This command is really useful and handy.
I use it everyday.

There are four flags of this command.
1. `--type`
2. `--network`
3. `--list-all`
4. `--show-prefix`

Back to the challenge.

We know Gavin's SS58 address. And we need to convert it into the public key.

Run:
```sh
subalfred key 13RDY9nrJpyTDBSUdBw12dGwhk19sGwsrVZ2bxkzYHBSagP2
```
Then we got:
```
0x6af08f6bb841825b168ddf79837e70d88d75e1c5b290b74fa97cedfd668dd22c
```

### [hash command](https://subalfred.hack.ink/user/cli/hash.html)
Sometimes, you might want to get the data's hash.

With Subalfred, you could run:
```sh
subalfred hash 0123
```
The command above is the same as:
```sh
subalfred hash 0x0123
```

Subalfred will handle the `0x` prefix for you.
You don't need to worry about the hex format.

And it provides 11 hashers.
If you don't specify `--hasher` it will use the default one, `blake2-128-concat`.
- blake2-128
- blake2-128-concat (default)
- blake2-256
- blake2-512
- twox64
- twox64-concat
- twox128
- twox256
- keccak256
- keccak512
- sha2-256

Back to the challenge, what should we do next?
```sh
subalfred hash 0x6af08f6bb841825b168ddf79837e70d88d75e1c5b290b74fa97cedfd668dd22c
```
Then we got:
```
0x54d2672c97d91c8edf30d6cd2dfc8db66af08f6bb841825b168ddf79837e70d88d75e1c5b290b74fa97cedfd668dd22c
```

---

Let's build the storage key.
```
0x26aa394eea5630e07c48ae0c9558cef7b99d880ec681799c0cf30e8886371da9 + 0x54d2672c97d91c8edf30d6cd2dfc8db66af08f6bb841825b168ddf79837e70d88d75e1c5b290b74fa97cedfd668dd22c
0x26aa394eea5630e07c48ae0c9558cef7b99d880ec681799c0cf30e8886371da954d2672c97d91c8edf30d6cd2dfc8db66af08f6bb841825b168ddf79837e70d88d75e1c5b290b74fa97cedfd668dd22c
```

Let's check if the result is the same as the PolkadotApps' one.

Finally:
```sh
curl -X POST -H 'Content-Type:application/json' https://rpc.polkadot.io -d '{"id":0,"jsonrpc":"2.0","method":"state_getStorage","params":["0x26aa394eea5630e07c48ae0c9558cef7b99d880ec681799c0cf30e8886371da954d2672c97d91c8edf30d6cd2dfc8db66af08f6bb841825b168ddf79837e70d88d75e1c5b290b74fa97cedfd668dd22c"]}`
```

### [convert command](https://subalfred.hack.ink/user/cli/convert.html)
**What** if you want to hash bytes data? Like `[0, 1, 2, 3]`.

With this command, we can convert the data between bytes and hex.
Let's have a try:
```sh
subalfred convert bytes2hex "[65, 117, 114, 101, 118, 111, 105, 114, 88, 97, 118, 105, 101, 114]"
```
```
0x41757265766f6972586176696572
```
```sh
subalfred convert hex2bytes 0x41757265766f6972586176696572
```
```
[65, 117, 114, 101, 118, 111, 105, 114, 88, 97, 118, 105, 101, 114]
```

Maybe you are not familiar with this name, byte string literal.
But I think you are familiar with this syntax in Rust:
```rs
let bytes = b"\x19Ethereum Signed Message:\n";
```
It's a `&[u8]`.
It's also an [EIP-191](https://eips.ethereum.org/EIPS/eip-191) signing message prefix.

Sometimes you might want to know its bytes style. So you could hardcode the bytes in other languages,
or you you might want to turn the bytes style into a human readable style.

Let's take a look at the examples:
```sh
subalfred convert bytes-style --from byte-string-literal --to vec-string "\x19Ethereum Signed Message:\n"
```
```
[25, 69, 116, 104, 101, 114, 101, 117, 109, 32, 83, 105, 103, 110, 101, 100, 32, 77, 101, 115, 115, 97, 103, 101, 58, 10]
```
```sh
subalfred convert bytes-style --from vec-string --to byte-string-literal "[25, 69, 116, 104, 101, 114, 101, 117, 109, 32, 83, 105, 103, 110, 101, 100, 32, 77, 101, 115, 115, 97, 103, 101, 58, 10]"
```
```
\x19Ethereum\x20Signed\x20Message:\x0A
```
You might found something different.
But do worry, `\x20` is ` ` and the `\x0A` is `\n`.
Try:
```sh
subalfred convert bytes-style --from byte-string-literal --to vec-string "\x19Ethereum\x20Signed\x20Message:\x0A"
```
```
[25, 69, 116, 104, 101, 114, 101, 117, 109, 32, 83, 105, 103, 110, 101, 100, 32, 77, 101, 115, 115, 97, 103, 101, 58, 10]
```

In the fist part, we use the storage-key command to calculate the storage key.
But let's try calculating the storage key with convert and hash.
As the formula said: `twox128(System) + twox128(Account)`
```sh
subalfred convert ascii2hex System
```
```
0x53797374656d
```
```sh
subalfred hash --hasher twox128 0x53797374656d
```
```
0x26aa394eea5630e07c48ae0c9558cef7
```
```sh
subalfred convert ascii2hex Number
```
```
0x4e756d626572
```
```sh
subalfred hash --hasher twox128 0x4e756d626572
```
```
0x02a5c1b19ab7a04f536c519aca4983ac
```
```
0x26aa394eea5630e07c48ae0c9558cef7 + 0x02a5c1b19ab7a04f536c519aca4983ac
0x26aa394eea5630e07c48ae0c9558cef702a5c1b19ab7a04f536c519aca4983ac
```
