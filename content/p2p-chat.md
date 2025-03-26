+++
title = "A Chat with an Ace Up Its Sleeve!"
date = "2025-03-26T20:00:00Z"

[extra]
author = "negrunch"
img = "/img/chat.jpg"
summary = "Mostro has implemented a new end-to-end encrypted chat for its Bitcoin P2P exchanges, designed to resolve disputes without compromising user privacy. Using advanced cryptography (DHEC), each transaction generates a unique *shared master key* known only to the buyer and seller. In case of a dispute, either party can voluntarily hand over this key to a mediator, allowing them to decrypt and review only that specific conversation, which is unalterable and cannot be deleted by scammers. This innovative feature ensures the availability of verifiable evidence for fair resolution, avoiding the need for centralized message storage and protecting the overall privacy of communications on Mostro."
+++

## Introduction: Speaking Clearly and Safely in the Bitcoin P2P World

Exchanging Bitcoin directly between people (peer-to-peer or P2P) offers freedom and control, eliminating intermediaries. At Mostro, we are committed to making this experience as smooth and secure as possible. We know that clear communication between buyer and seller is fundamental, especially when things don't go as planned.

But what happens if a dispute arises? How can we ensure the truth comes to light without compromising anyone's privacy? Today we present a new feature in Mostro designed exactly for that: an **integrated, end-to-end encrypted chat, with an ace up its sleeve to resolve disputes fairly and transparently.**

## The Dilemma of Disputes: Deleted Messages and Privacy at Risk

In our almost four years of experience working with [@lnp2pBot](https://lnp2pbot.com/), we encountered a recurring and frustrating problem: when one of the parties tried to scam the other, they often deleted the messages from the conversation. Poof! The evidence disappeared, leaving the honest user unable to prove what happened and greatly hindering the fair resolution of the dispute.

The "easy" solution would be for us to use the bot as an intermediary for each message and store a copy of all conversations in a central database. That way, an administrator could simply review the history in case of a dispute. But let's be honest, **that would be terrible in terms of privacy**. It would go against the decentralized and private spirit of Bitcoin, exposing conversations that should be confidential. We needed a better solution.

## Mostro Chat: Private Communication by Default

That's why we've implemented a chat system directly within Mostro clients. When the buy/sell operation advances to an active status, a direct and private communication channel opens with the other party.

This chat uses the **Nostr** protocol for message transfer, ensuring that communication travels in a decentralized and censorship-resistant manner. More importantly, the conversation is **end-to-end encrypted**. This means that only you and the other person involved in the transaction can read the messages. Not even us at Mostro can know what you are talking about, much less see what is being said. So far, it's the privacy you would expect.

## The Innovation: The "Shared Master Key" for Disputes

This is where things get interesting and radically different. For each operation on Mostro, the system uses advanced cryptography (specifically, a process called **Diffie-Hellman over Elliptic Curves or DHEC**) so that you and your counterparty generate, independently but in a coordinated manner, a **unique shared secret key**.

Think of it as if you each wrote a message on a piece of paper and put it in a safe specific to that order. Thanks to this cryptographic "magic," both the buyer and the seller obtain an identical copy of the key for *that specific safe*, without needing to send it directly between parties! **Only both parties know that key**. It is unique to that conversation and that operation.

## Resolving Disputes Without Breaking Privacy

Now, what happens if there is a disagreement? Suppose the seller claims not to have received the fiat payment, or the buyer says they did send it. This is where the "shared master key" comes into play:

1.  **A Dispute Arises:** One of the parties initiates the dispute process in Mostro.
2.  **Voluntary Decision:** Either party (buyer or seller) has the option to **voluntarily share** their copy of the "shared master key" with the person designated to resolve the dispute (the mediator).
3.  **Controlled Access:** With this unique key, the mediator can "open" the digital safe and **decrypt only the conversation corresponding to *that specific transaction***.
4.  **Immutable Evidence:** The messages within this chat are recorded in such a way that they cannot be deleted or altered without it being evident. The mediator can see the conversation as it happened, verifying who said what and when. This makes it extremely difficult for a scammer to get away with it if the evidence is in the chat.

## Why is This Revolutionary?

This solution achieves the best of both worlds:

* **Privacy by Default:** Your conversations are private and encrypted. No one can spy on them.
* **Transparency on Demand:** If a problem arises *and* one of the parties consents, the evidence can be securely revealed *only* to the mediator and *only* for that dispute.
* **Anti-Manipulation Security:** Messages cannot be deleted or falsified by a scammer to hide their actions.
* **Decentralization:** We don't depend on storing your private chats on our servers.
* **Unique Keys per Transaction:** A crucial detail is that Mostro generates new cryptographic keys for each order. This means that even if you trade with the same person again, the "shared master key" for that new conversation will be completely different. The privacy and security of each operation are independent.

## Conclusion: A Safer and Fairer Future for P2P

With this implementation in the Mostro chat, we are taking an important step towards strengthening trust and security in Bitcoin P2P exchanges. We combine robust cryptography with an intelligent and privacy-respecting mechanism to ensure that disputes can be resolved as fairly as possible, easily exposing those who try to act in bad faith.

We want you to feel safe and supported when using Mostro, knowing that you have innovative tools designed to protect you without compromising your data.

## Interested in the Technical Details?

For those with more technical inclinations who want to delve deeper into the cryptography behind the generation of this shared key, you can consult our detailed article here: [https://mostro.network/protocol/chat.html](https://mostro.network/protocol/chat.html)

You can also try **mostro-chat** which is a proof-of-concept and see for yourself how what you have read works.

[https://github.com/MostroP2P/mostro-chat](https://github.com/MostroP2P/mostro-chat)