# Demystifying Macro Magic

* ⚡️ Intermediate
* 👤 Presenter: Sam (FRAME core developer at Parity)
* 📆 Date scheduled: November 22, 2022

👉 [Join the livestream on Twitch](https://www.twitch.tv/polkadotdev) to participate and get your questions answered.

### Description

In this seminar, we are joined by Parity core FRAME developer, Sam who's been working some key FRAME macro features (see [#12536](https://github.com/paritytech/substrate/pull/12536) and [#12536](https://github.com/paritytech/substrate/pull/12536)). He  will be explaining the high level of how the FRAME pallet macro parsing and expansion works through the lens of implementing a simple pallet macro.

### Topic

FRAME macros

### Plan

1. A brief overview of what pallet macros are and where they are used.
2. A quick description of the `whitelist_storage` macro, what it is supposed to do, and why it should exist.
3. A general discussion about the "outer macro" pattern.
4. Going through the steps of implementing the `whitelist_storage` macro as a way of explaining how pallet macros are parsed and expanded.
5. (time permitting) How pallet macros are tested.

### Links and resources

- [FRAME Macros](https://docs.substrate.io/reference/frame-macros/)
- [`cargo expand`](https://github.com/dtolnay/cargo-expand)
- [Macros - The Rust Reference](https://doc.rust-lang.org/reference/procedural-macros.html)
- [Macros - The Rust Book](https://doc.rust-lang.org/book/ch19-06-macros.html)
- [AST (Abstract Syntax Tree) - Wikipedia](https://en.wikipedia.org/wiki/Abstract_syntax_tree)