# Chasing the Block: Developing Elegant UI Applications for Substrate

## Context

Developing elegant and innovative UI applications for the Substrate ecosystem is an extremely challenging and equally rewarding endeavor. This proposed seminar is broadly about my experience and learnings (and troubles 🤭) so far as an application developer for the Substrate ecosystem in the last ~1.5 years, and how they could hopefully apply to this much relevant field.

Before being introduced to the blockchain industry through a hire in late 2019, I had about 16 years of experience in professional software development and leadership spanning a variety of contexts such as enterprise middleware and application development, defence industry and fintech applications, microchip and sensors development for art installations, iOS and Android development for startups, and more. And at my last hire, I stacked another 1.5 years' experience leading an iOS & Android development team that successfully delivered a slick cryptocurrency wallet application.

So by the time I discovered the Substrate ecosystem in early 2021 I had enough reasons to think that I was experienced enough to pull off any kind of development in any kind of setting with relative ease. Little did I know what was coming 😏

# Seminar content

## 1. Introduction

- Short story of me as a software developer.
- My introduction to the Substrate ecosystem through the Thousand Validators Programme (1KV), initial impressions and experience.

## 2. Brief: What I've Been Building, and Why

A quick chronological go-through of the projects I've built and am currently building, and why and for whom they are built.

- [1KV Telegram Bot](https://github.com/helikon-labs/polkadot-kusama-1kv-telegram-bot)
- [Substrate Validator Toolkit (SubVT)](https://github.com/helikon-labs/subvt-backend)
- [ChainViz](https://github.com/helikon-labs/chainviz)
- Rewrite of the 1KV Bot as the [SubVT Telegram Bot](https://github.com/w3f/Grants-Program/blob/master/applications/subvt-telegram-bot.md)

## 3. A Deeper Technical Dive

### 1KV Telegram Bot ([🔗](https://github.com/helikon-labs/polkadot-kusama-1kv-telegram-bot))
- Why and how I developed it, and the community reception.
- How it works.

### SubVT ([🔗](http://subvt-test.helikon.io/) landing demo)
- What it is, who it is for and why there is a need for it.
- Coming up with the idea, and the Kusama Treasury grant [application](https://docs.google.com/document/d/1mCD1lRoEwbV3Xp5N-HzEKA0KROCmNkMFInLGd4nAz-k/edit?usp=sharing) process.
- System [architecture](https://github.com/helikon-labs/subvt/blob/main/document/software/01-subvt_system_architecture.md) choices.
- Developing the backend services, and monitoring them.
- Explanation of how the [SubVT backend](https://github.com/helikon-labs/subvt-backend) is becoming the enabler for multiple future projects.
  - ⚗️ **Workshop:** A quick hands-on that demonstrates SubVT's WS-RPC and REST services as enablers for application development.
- Developing the Android and iOS data access libraries, and applications.
- Finding [Klad](https://klad.design), the design team, and getting the UX and UI design work completed.
  - Initial briefing [documentation](https://docs.google.com/document/d/1gVGHBSqji-XJc6luvLDm3ilq08LMVb2hhC3EqZ5jr5Q/edit?usp=sharing) for the designers and introductory calls.
  - [Branding](https://drive.google.com/file/d/1Bwn919_43cp30fwmVazKl8BEoCmetw6L/view?usp=sharing).
  - [UX mapping](https://www.figma.com/file/XzSssIXskyo8aMTc1myClC/?node-id=178%3A350), [UX design](https://www.figma.com/file/XzSssIXskyo8aMTc1myClC/?node-id=0%3A1) and [UI design](https://www.figma.com/file/XzSssIXskyo8aMTc1myClC/?node-id=178%3A603).
  - Design [documentation](https://drive.google.com/file/d/1sZUt4GM0ghOm0bAdAEWUMF-ujsfR_Zbo/view?usp=sharing) and [assets](https://github.com/helikon-labs/subvt/tree/main/assets/design).

### ChainViz ([🔗](https://alpha.chainviz.app))
- What it is, who it is for and the purpose it serves.
- Alpha version UI explanation, visualization challenges and choices.
- How it works with the SubVT backend services and the Polkadot JS library.
- Short and long-term plans for ChainViz.

## 4. Challenges, Thrills and Joys: The Psychology and Environment of Developing for Substrate

This section is mainly about the development experience. Focus is on developing beautiful, user-friendly UI applications for the Substrate ecosystem, especially in comparison to typical web/desktop/mobile development in a typical startup or enterprise setting.

- Why it is much harder, but also way more rewarding and educational than typical web/desktop application development.
- Software development challenges, and getting used to **chasing the block** and the runtime 🏃🏻‍♂️.
- UI, UX and product development challenges.
- Tools of the trade.
- The demand for constant novelty, how it can get seriously exhausting, and how to deal with it and avoid extreme hair-loss:P
- ⭐  The amazing community factor, and W3F & treasury grant programs.

## 5. Future Projects

- **PolkaZen**, the governance-focused Polkadot (Substrate) citizen application.
- **ChainSynth**, an audio-visual synthesizer with real-time multi-chain data as input, targeted for audio-visual artists and enthusiasts.


## 6. Q&A

Closing Q&A session, possibly with code examples.