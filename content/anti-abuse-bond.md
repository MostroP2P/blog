+++
title = "The Anti-Abuse Bond: Putting Honesty Up as Collateral"
date = "2026-06-17T12:00:00Z"

[extra]
author = "catrya"
img = "/img/anti-abuse-bond.jpg"
summary = "One of the great challenges of a decentralized, censorship-resistant, and private P2P system like Mostro is mitigating abuse: spam in the order book and the scam attempts of those who can create a brand-new identity in seconds. That's why we added an optional mechanism: the anti-abuse bond. When entering a trade, the user locks a small amount of sats as collateral that they get back in full if they act in good faith, but which they lose if they try to scam or abandon the trade. It is a second hold invoice, independent from the escrow, and each node decides whether to enable it and under what conditions, according to the characteristics of its community."
+++

Building a decentralized, censorship-resistant, and private P2P exchange system on Nostr, like Mostro, comes with a hard challenge: how do you mitigate abuse?

A malicious user can try to flood a Mostro's order book with spam offers, just to be a nuisance and bury the real offers in the noise. Or the other way around: empty the book by taking every offer just so they vanish. And since Mostro is anonymous —and creating a new identity is as easy as generating a key pair—, how do you protect users from those who want to scam?

It's true that we already have solid defenses: there is a dispute system, and the escrow's hold invoice is not released until the seller confirms they received the fiat. A scammer, therefore, rarely achieves their goal. But something was missing: until now, trying cost nothing. Whoever tried and failed would simply try again.

## A decision that took us time

We had been thinking about an anti-abuse bond for a while, but what held us back was this: if someone completely new wants to buy sats, how are they going to pay a bond if they don't have sats yet?

The answer was not to impose it. We decided this feature would be **optional**: each Mostro node administrator can enable it or not, and set whatever conditions they see fit according to the characteristics of their own community. A node aimed at newcomers can do without it; another one, more exposed to abuse, can turn it on. The network decides, not us.

## What is the anti-abuse bond?

The idea is the same as a rental deposit. When you rent an apartment they ask you for a security deposit: if you return everything in order, you get it back in full; you only lose it if you break something. It works because it aligns incentives —you take better care of what you know could cost you.

In Mostro, when entering a trade you put up a small amount of sats as collateral that you get back **in full** if you act in good faith, but which you lose if you try to scam your counterparty or fail to do your part. The consequence is direct: a scammer no longer plays for free. They now put **their own money at risk**, and that discourages abuse before it happens.

## Each node sets its own rules

Remember that Mostro is not a single server, but many nodes competing with each other. Each node that enables the bond defines its own rules: who it asks for it (whoever creates the order, whoever takes it, or both) and how much it is. The amount is usually a small percentage of the order value —for example, **1%** with a minimum in sats—, but that percentage is decided by each node.

> **Tip:** You can check whether the node you are using requires an anti-abuse bond —and how much it would be— from your own Mostro client, in the *About* section, before trading.

## Isn't it the same as the escrow?

No. The bond is completely independent from the trade escrow. It is a second hold invoice: your sats are only locked in your wallet, they are not spent. If everything goes well, they are unlocked and returned to you without ever having left your wallet. It is not mixed with or deducted from the trade amount.

So, under normal conditions, the bond is not a cost: it returns to your wallet in full, just like the sats locked in any hold invoice.

## When do I get my bond back?

You get **100%** back as long as you do your part:

- You complete the trade correctly.
- You cancel the order cooperatively.
- A dispute arises and the administrator does not determine that you acted in bad faith.

## And when can I lose it?

You only lose your bond for trying to abuse the system. There are two situations:

1. **By decision in a dispute.** An administrator (*solver*), after reviewing the evidence, determines that you acted in bad faith and instructs Mostro to claim your bond.
2. **By failing to do your part and letting the time run out.** If you take or create an order and then do not pay the order's hold invoice or do not provide your invoice in time, you let the deadline that was your responsibility expire. This only applies if the node enabled that policy.

## Where do the sats from a claimed bond go?

When a bond is claimed by decision in a dispute, the sats are split between the node —which thereby funds the work of resolving disputes and keeping the service running— and the honest counterparty, as compensation for the harm. The proportion of that split is defined by each node and is public, so you can know it before trading.

If instead it is claimed for letting the deadline expire, the sats go to the node.

## Let's see it with an example

> **A seller who wants to keep it all.** Carlos creates a sell order (he is the **seller**) and Diana takes it to buy sats (she is the **buyer**), on a node that requires an anti-abuse bond. Diana makes the fiat transfer correctly and keeps the receipt. But Carlos, in bad faith, refuses to release the sats and claims he never received the payment, hoping to keep both the fiat and the sats.
>
> Diana opens a dispute and presents the administrator with the receipt for the transfer. The *solver* confirms that Diana paid: Mostro releases the escrow sats in her favor and **claims Carlos's bond**. As compensation for the trouble, Diana receives a share of that bond; the rest goes to the node. Carlos not only failed in his scam, but lost his own money for attempting it.

> **Someone who takes an order and disappears.** Eduardo takes an order to buy sats and Mostro asks him for the next step to continue. But Eduardo simply stops responding: he doesn't pay, doesn't move forward, doesn't cancel. His counterparty is left hanging, waiting for someone who is never going to show up.
>
> On a node that enabled the deadline policy, there's no need to open any dispute: when the time that was Eduardo's responsibility runs out, he **loses the bond for that trade** automatically. This way, abandoning a trade halfway stops being free, and whoever is acting seriously is not left stuck waiting indefinitely.

## If you are owed your counterparty's bond

If your counterparty loses their bond and you are owed a share, your client will ask you for an invoice to send you those sats. You have a window defined by the node (for example, **15 days**) to claim it; if you let it pass, you lose the right to collect that share. That is why it is best to attend to your client's request as soon as it appears.

## Conclusion

The anti-abuse bond pursues a clear goal: making acting in good faith the natural thing in Mostro, and making abuse expensive, without sacrificing privacy or decentralization. Whoever does their part pays nothing; whoever abuses, pays. And since each node decides its own rules and makes them public, you always choose with the information in front of you.

## More information

- **User documentation:** [Anti-Abuse Bond](https://mostro.network/docs-english/anti-abuse-bond.html)
- **Technical specification:** [ANTI_ABUSE_BOND.md](https://github.com/MostroP2P/mostro/blob/main/docs/ANTI_ABUSE_BOND.md)
- **Protocol documentation:** [Add Bond Invoice](https://mostro.network/protocol/add_bond_invoice.html)

Trade with peace of mind: in Mostro, honesty always comes back to you in full! 🧌🫶
