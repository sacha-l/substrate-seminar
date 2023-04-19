# Tuxedo: Substrate Runtimes with the UTXO model

* ⚡️ Intermediate
* 👤 Presenters: Joshy (Blockchain Chef) and Andrew (Blockchain Connoisseur)
* 📆 Date scheduled: April 18, 2023 (4PM CET)

👉 [Join the livestream on Twitch](https://www.twitch.tv/polkadotdev) to ask questions and hang out in the chats!


### Description

In the blockchain space their are two main models for creating chain logic. 
The account model like in Ethereum and Polkadot, and the UTXO model like in Monero and Cardano.

Substrate runtimes have traditionally been written in FRAME which uses the account model. 
But Substrate itself is general enough to support either. Enter Tuxedo. 
Tuxedo is an alternative to FRAME that allows developers to write Substrate runtimes in the UTXO model.

### Topic

Runtime Development

### Plan

This Seminar will cover foundational concepts, discuss the UTXO model theory, live code a UTXO based runtime including unit tests with Tuxedo, and play with the resulting chain.

* Explore Substrate's client/runtime boundary
* Clarify that FRAME is just for the Runtime, has assumptions, and is not a necessary part of a Substrate Chain
* Compare and contrast the accounts model and the UTXO model
* Look at the Tuxedo architecture and Tuxedo template node
* Live code a Runtime using Tuxedo. (I'm thinking maybe an order-book dex or a TCR, but open to suggestions.)
* Start up and play with the resulting chain.

### Links and resources

- Tuxedo repository: https://github.com/Off-Narrative-Labs/Tuxedo/
- W3F Grant: https://github.com/w3f/Grants-Program/blob/master/applications/tuxedo.md
- Slides: https://off-narrative-labs.github.io/Substrate-Seminar-april-2023
