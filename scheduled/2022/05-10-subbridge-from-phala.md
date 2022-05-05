# A multi-bridge router bridging Dotsama and other ecosystems

## Description

SubBridge is a multi-bridge router dedicate to connect the Polkadot parachains and other ecosystems. By first integrating two popular bridge solutions, i.e., ChainBridge and CelerBridge, it connects Dotsama and EVM ecosystems, and will bridge more ecosystems in the future.

The core of SubBridge is two-fold: 1) it uses common interfaces to represent different blockchains and the assets on them, which makes it a "bridge hub" and able to integrate different bridges; and 2) it designs an asset router across bridges, which means it can forward assets from one bridge to another to achieve the cross-chain transfer even if there is no direct bridge.

As its first version, SubBridge chooses to integrate XcmBridge (a bridge between parachains) and ChainBridge (a bridge between Khala network and other EVM chains). It utilizes the `MultiLocation` concept introduced by XCM protocol to represent the cross-chain route path. By implementing a bridge router, SubBridge can forward transfer from one bridge to other bridge. That means users can transfer assets from parachains to EVM chains directly, and vice versa.

![](https://i.imgur.com/jDBacn1.png)

So far with SubBridge, people can transfer assets between:

- Khala <-> Parachians
- Khala <-> EVM chains
- **Parachains <-> EVM chains**

## Seminar plan

* What is SubBridge
* Why we built it
* Implementation of SubBridge (e.g. router, spec design)
* How to integrate your assets into SubBridge
* Further development plans

## Next steps for SubBridge

- Integrate CelerBridge [WIP]
- Upgrade ChainBridge to V2
- Upgrade XCM to V3

## Relevant material

* [SubBridge Tech Talk Slide](https://docs.google.com/presentation/d/1BpcSxCA8kyA5oU75mzkh-Om6rbu5EOIQy9V2Ged4lXg/edit?usp=sharing)

* [SubBridge Wiki](https://wiki.phala.network/en-us/general/subbridge/intro/)