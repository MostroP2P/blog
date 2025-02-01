+++
title = "Keys management on Mostro"
date = "2025-02-01T12:00:00Z"

[extra]
author = "negrunch"
img = "/img/gift.png"
summary = "Keys management on Mostro is based on a security system as simple as exchanging wrapped gifts and changing safe combinations: each message between the user and the platform uses ephemeral keys that function as *disposable locks* while each buy or sell order is linked to a different key derived from a unique seed, ensuring that the information and transactions are always protected."
+++

Keys management on Mostro might sound complicated if you have never dealt with technical concepts related to security and cryptography. However, we will explain it with examples you might encounter in your everyday life. It’s easier than it seems!

## Imagine Sending a Wrapped Gift

Let’s think of key management as the process of exchanging [wrapped gifts](https://github.com/nostr-protocol/nips/blob/master/59.md). When you send a gift to someone, you want to make sure that only that person can open it. In the world of Mostro, these gifts are the data you send, and the wrapping is the layer of security that protects them.

In this case, the keys are like the secret combinations needed to open that wrapping. Mostro uses an ephemeral key for each message sent between the client and the platform. These ephemeral keys, an essential feature of the **gift wraps**, ensure that each message is protected individually and uniquely.

## Key Rotation: Changing the Lock for Each Operation

Suppose that in the physical world you need to exchange a package with Bob. For this, Bob and you must exchange several confidential letters to agree on how to make the exchange. For this operation, you will use a different identity than the one you use in your subsequent transactions with other users. Even if you were to transact with Bob again, both of you would be using distinct identities. That’s what Mostro does with key rotation!

Each time a user creates or takes a buy or sell order, a new key specific to that operation is generated. These keys are derived from a seed that the client randomly generates for the user. From this seed, many keys can be derived: the public key at index `0` (derivation path `m/44'/1237'/38383'/0/0`) acts as the main identifier with Mostro, while the keys with indices starting from `1` (for example, `m/44'/1237'/38383'/0/n`) are the ones rotated for each new order. This way, even though the key for an operation remains constant while the operation lasts, once it is completed a new key is used for the next order, ensuring additional security.

## Ephemeral Keys: Disposable Locks for Unique Messages

Now imagine that you need to send an important letter by mail, but you don’t want to use your usual lock to protect it. Instead, you use a disposable lock that is only useful for that particular delivery. Once the letter reaches its destination, the lock is no longer of use.

In Mostro, ephemeral keys work in a similar way. They are keys created to protect data for a short period or for a specific purpose, such as an individual message between the client and Mostro. Once the message is processed, that key is destroyed and cannot be used again. This minimizes the risk of someone taking advantage of a compromised key.

## Reputation vs. Full Private Mode

Mostro allows users to choose between two operating modes: **reputation** and **full private mode**.

- **Reputation Mode**: As mentioned earlier, users identify themselves to Mostro with the public key at index `0` (`m/44'/1237'/38383'/0/0`). This allows for the reputation to be tied to this key. Only Mostro and the user know this public key, ensuring the user’s privacy. Mostro takes care of calculating the reputation based on the counterparty's rating.

- **Full Private Mode**: This mode allows users to operate without needing to send an identifying key. In this way, Mostro cannot link orders from the same user, which guarantees the highest level of privacy and security. Due to the private nature of this mode, it is not possible to maintain a reputation for the user.

## Why Is This Important?

Think about how hard you work to protect something valuable, like a confidential document or a special gift. Key management on Mostro ensures that all the information and operations carried out are protected at the highest level. By combining the use of ephemeral keys to protect each message and key rotation for each operation, Mostro guarantees that your data is always safe.

## Conclusion

In summary, key management on Mostro can be understood as the art of using unique, temporary, and specific security combinations to keep your data protected. Whether using ephemeral keys for individual messages or rotating keys derived from a seed for each order, the system is designed to offer peace of mind and security in every interaction.

Now you know that Mostro not only protects your data but does so efficiently and carefully, as if every piece of data were a wrapped gift just for you!

## More Information

**Keys Management in the Mostro Protocol**: [https://mostro.network/protocol/keys-management](https://mostro.network/protocol/keys-management)
