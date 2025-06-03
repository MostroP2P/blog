+++
title = "Identity Keys encryption on Mostro"
date = "2025-05-30T12:00:00Z"

[extra]
author = "arkanoider"
img = "/img/Data_Encryption.jpg"
summary = "Identity keys are now detached from users, ensuring that order identity keys are encrypted. This means that even in the event of a database leak, there is no direct correlation between users and their orders. By implementing this separation, we enhance user privacy and security, making it significantly more challenging for unauthorized parties to link sensitive information back to individual users. This approach not only protects user identities but also fosters trust in the platform, as users can engage with confidence knowing their data is safeguarded."
+++

Hey Mostro fans! 👋
We've got some exciting news for all you privacy-conscious folks out there: Mostro Core just got a major upgrade in how it keeps your most important secrets safe. Let's talk about the brand new database encryption option, why it matters, and how it works in simple terms.

## What's New?

In today's digital world, protecting sensitive information is more important than ever, especially in decentralized platforms like Mostro. That's why we're excited to announce a major upgrade in how Mostro Core keeps your secrets safe.

Starting now, when an admin launches Mostro, they'll see a friendly prompt:

> **"Do you want to password encrypt your database?"**

With a simple yes or no, the admin decides if they want to add an extra lock to the most sensitive info. If they choose to password-protect, the identity/master key—also known as the index 0 key—is encrypted and can only be accessed with the admin's password.

This password is only required for the Mostro admin, and the encryption process is totally transparent for clients connecting to the daemon. Clients don't need to worry about any extra steps!

---

## Why Should You Care?

Here's the cool part: Mostro now separates your order keys and reputation from your identity/master key. With this update, your master key (index 0) is stored safely with password-based encryption. This means that your orders and your reputation cannot be easily linked back to your identity—even if someone were to access your database file, it would be extremely difficult to connect the dots without your password.

- **Extra Privacy:** Your identity/master key is shielded, so your orders, actions, and even your reputation can't be easily linked back to you.
- **Peace of Mind:** If your database leaks, your most important key remains safe behind your password.
- **Simple Choice:** The admin is in control. Want that extra security? Just say yes at startup!

Curious about how identity keys work and why they're important? Check out our previous blog post: [Identity Keys Management](https://mostro.network/blog/keys-management/)

---

## Who Should Use This?

This feature is especially for Mostro admins who are really passionate about protecting users' privacy and passwords. If you're an admin who cares deeply about safeguarding your users' sensitive info, this option is for you! It's perfect for both power users and anyone just getting started with Mostro. If you want to keep your digital identity locked down, you'll love this.

---

## How Does It Work? (Without the Jargon)

- On the first launch after updating, Mostro asks the admin if they want to set a password.
- If they set one, the identity/master key (index 0 key) is encrypted and safe—think of it like putting your passport in a locked safe.
- The password is managed by the Mostro admin and is used to encrypt specific columns in the daemon's database. This entire encryption process happens behind the scenes and is totally transparent for clients using Mostro—no extra steps required!

---

## A Peek Under the Hood: How Encryption Works

Okay, here's a quick look for the curious minds who want to know what's going on behind the curtains:

- When the admin sets a password, Mostro uses a technology called Argon2 to create a super-strong, unique encryption key just for you. (It's like making a brand new, strong lock every time, using your password as the blueprint.)
- For each order, a different, salted encryption key is derived—so even if someone somehow cracked one, they wouldn't get access to the others.
- These keys are then used to encrypt your data using a secure algorithm called ChaCha20-Poly1305.
- Finally, the encrypted result is converted to a machine-friendly ASCII string using Base64, making it easy for computers to store and handle—but impossible to read without the password.

You don't have to remember any of this technical stuff, but it's nice to know that you're getting some cutting-edge protection behind the scenes!

---

## The Bottom Line

We believe privacy should be easy and accessible. With this new database encryption, Mostro Core helps you keep your identity key truly yours, and makes sure your orders and reputation stay private. So next time you're asked about password-protecting your database, go ahead and give it a try!

Stay safe out there, and happy trading! 🚀

---

*Questions or thoughts? Drop them in our [Telegram chat](https://t.me/MostroP2P)*
