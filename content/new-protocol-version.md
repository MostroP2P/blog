+++
title = "A New Version of the Mostro Protocol"
date = "2026-06-18T12:00:00Z"

[extra]
author = "negrunch"
img = "/img/vesion2.jpg"
summary = "Version 2 of the Mostro protocol leaves gift wraps (NIP-59) behind for messaging between Mostro and clients, adopting instead kind 14 events with content encrypted via NIP-44. This change closes the attack window we nicknamed the \"Gift Wrap Apocalypse\", a spam vector that, anyone could use to take down a Mostro node, without sacrificing privacy, since we keep rotating keys for every order. The improvement ships in version 0.18.0 of the Mostro node and, together with the anti-abuse bond, makes Mostro ready for production."
+++

## How we started

When we began working on Mostro, we had to decide how clients and the Mostro node would communicate. Our first experiments used NIP-04, which we used to encrypt data on Nostr; at that time NIP-04 was the standard.

NIP-04 had a problem: it leaked user information, and that information could help third parties deanonymize them. Since in Mostro's early days a user could publish orders using any private key, we started to notice that some users were using the same private key they posted with on clients like Amethyst, Damus, etc., which was far more terrible for their privacy.

We immediately started working on a solution that would keep the user protected without hurting the clients' UX. So we thought, implemented, rethought, and reimplemented the first version of the protocol.

## The first version: gift wraps and key rotation

We decided to use gift wraps (NIP-59), which fit us like a glove since they hid data such as the origin of the message: each message is sent with an ephemeral key. Even so, we still had a problem. The messages Mostro sent to the client were addressed to a unique user pubkey, and if users were using the same pubkey they posted with on Damus, it would be very easy to link them to Mostro.

So we decided to create a key rotation system. Instead of letting the user enter a private key, we made the clients generate a seed (BIP-39) and, from there, the client would generate a key for every order the user created or took, in the purest Bitcoin wallet style (BIP-32).

The implementation wasn't simple, but the result was that the user obtained a high degree of privacy.

## The "Gift Wrap Apocalypse"

In theory this works very well, but using gift wraps on Nostr opens an attack window against relays and Mostro nodes. I call this attack the "Gift Wrap Apocalypse".

Since gift wraps are sent with ephemeral keys and a modified timestamp, an attacker can send any number of these events with garbage inside, spamming, and until Mostro decrypts them it won't know whether they are legitimate events or not. This makes resisting these attacks very costly, because decrypting requires Mostro's resources. In theory it's very easy to take down a Mostro node by sending a large number of these events; now, with AI, any script kiddie with no technical knowledge can attack a Mostro node until it's left unable to respond.

So far we haven't received this dreaded attack, but before it happens we've gotten ahead of it and decided to drop gift wraps for messaging between Mostro and clients. Yes, we removed a layer of privacy, but, to be honest, by rotating keys for each order we still maintain a high degree of privacy when operating on Mostro.

## The solution: kind 14 + NIP-44

Instead we use kind 14 events with encrypted content (NIP-44). Just like that, as simple as that. We've gone from having encrypted content like this:

```json
// external wrap layer
{
  "id": "<id>",
  "kind": 1059,
  "pubkey": "<Buyer's ephemeral pubkey>",
  "content": {
    // seal
    "id": "<seal's id>",
    "pubkey": "<index 0 pubkey (identity key)>",
    "content": {
      // rumor
      "id": "<rumor's id>",
      "pubkey": "<Index 1 pubkey (trade key)>",
      "kind": 1,
      "content": [
        {
          "order": {
            "version": 1,
            "id": "<Order Id>",
            "trade_index": 1,
            "action": "take-sell",
            "payload": null
          }
        },
        "<index 1 signature of the sha256 hash of the serialized first element of content>"
      ],
      "created_at": 1691518405,
      "tags": []
    },
    "kind": 13,
    "created_at": 1686840217,
    "tags": [],
    "sig": "<index 0 pubkey (identity key) signature>"
  },
  "tags": [["p", "<Mostro's pubkey>"]],
  "created_at": 1234567890,
  "sig": "<Buyer's ephemeral pubkey signature>"
}
```

To this:

```json
[
  {
    "order": {
      "version": 2,
      "id": "<Order Id>",
      "trade_index": 1,
      "action": "take-sell",
      "payload": null
    }
  },
  "<index 1 signature of the sha256 hash of the serialized first element>",
  ["<index 0 pubkey (identity key)>", "<index 0 identity proof signature>"]
]
```

I won't dive into technical details, since you can see this in the [protocol documentation](https://mostro.network/protocol/key_management.html).

## Versioning and availability

This improvement ships in version 0.18.0 of the Mostro node. From there, version 1 of the protocol is deprecated but can still be used. In version 0.19.0, Mostro's default protocol option will be "2", and every trace of version "1" will be removed: enough time for all Mostro clients to update.

With this improvement, together with the [anti-abuse bond](https://mostro.network/blog/anti-abuse-bond/), we consider Mostro ready to be used in production. Always keeping in mind that it's experimental software and surely has bugs to fix, but we trust we have a stable product that provides solutions to those who need to be able to buy and sell Bitcoin freely, without fear of censorship, retaliation, or surveillance.
