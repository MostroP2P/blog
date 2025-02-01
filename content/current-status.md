+++
title = "Current status on Mostro"
date = 2024-12-20

[extra]
author = "negrunch"
img = "/img/first-post.webp"
summary = "Over the past year, Mostro has made significant strides in key management (rotating keys for each trade and improving privacy), standardizing orders on Nostr through the new NIP-69, and consolidating its ecosystem thanks to participation in the b4os residency, the creation of the Mostro Foundation, and the development of libraries (mostro-tools) and new clients (a mobile app and the Mostrui terminal interface). All of this aims to provide a privacy-focused, user-friendly peer-to-peer exchange platform, supported by HRF, Opensats, and other contributors."
+++

Since more than a year we've been tirelessly working on Mostro, here is a brief summary.

## Keys management

We have a lot of improvements and probably one of the most important is the final design of keys management, we started to discuss this idea in the previous quarter and we commented it in the last report, keys management is a way clients rotate keys for every trade adding another privacy layer to gift wrap previous implementation, more detailed info here. Today we've merged our main [PR](https://github.com/MostroP2P/mostro/pull/398) for implementing it on mostrod, we also implemented it on [mostro-core](https://github.com/MostroP2P/mostro-core/pull/67/files) and [mostro-cli](https://github.com/MostroP2P/mostro-cli/pull/89).

## New Nostr NIP merged

We also had our first official NIP merged, [NIP-69](https://github.com/nostr-protocol/nips/blob/master/69.md), with this we aim to standarize all orders from peer-to-peer platform on Nostr to have a big liquidity pool easily filterable.

## B4OS

Mostro was one of the projects participating in the [b4os residency](https://www.libreriadesatoshi.com/b4os), which took place in Buenos Aires right after this year’s [LABITCONF](https://www.labitconf.com/).

I participated as a mentor, going there daily for the whole program, helping developers get started on Mostro. Mostro received a lot of attention and had the largest number of contributors working on it (8 in total). We had two very productive weeks where we refined how Mostro will handle privacy and reputation at the same time. This will required some changes to mostrod and improvements to the [protocol documentation](https://mostro.network/protocol/), for which we (fingers crossed) now have a final version.

During the b4os residency, we received [contributions](https://github.com/MostroP2P/mostro-regtest/pull/2) that improved our Docker Mostro containers—amazing work that you can see [here](https://github.com/MostroP2P/mostro-regtest).

## Mostro foundation

We also made progress on establishing the Mostro Foundation, which will serve as a legal entity to handle donations and direct them to developers who want to contribute. Another [contributor](https://github.com/MostroP2P/mostro-foundation-website) created the [Mostro Foundation website](https://mostro.foundation/).

## Mostro-tools

We already have contributors working on [mostro-tools](https://github.com/MostroP2P/mostro-tools), a TypeScript library implementing the [Mostro protocol](https://mostro.network/protocol/).

## Mobile app

Our past attempt of building the mobile app failed, the developer quit, so we found another dev, third time's the charm. Now we’re moving forward with the mobile app, which is being developed by developer called Biz. Working on Mostro is a bit complex because we focus on privacy and censorship-resistance, and our main goal is to deliver these privacy features in an easy-to-use application. I want this app to be very intuitive, suitable even for non-technical users. Biz, delivered a first functional mobile app we can see all the work [here](https://github.com/MostroP2P/mobile/pull/31) and [here](https://github.com/MostroP2P/mobile/pull/33), we tested it and it works :D

## Mostrui

Finally we started another client, a Terminal User Interface (TUI) which is helping us to implement and understand problems that client developers can find on the process of building a client, this client is called [Mostrui](https://github.com/MostroP2P/mostrui).

All this couldn't be possible without the support of [HRF](https://hrf.org/) and [Opensats](https://opensats.org/) and all collaborators <3
