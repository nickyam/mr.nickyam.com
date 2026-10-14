---
title: "Hardware Wallets Are Not a False Proposition"
date: "2026-10-12T12:02:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Hardware Wallet"
  - "Self-Custody"
  - "Cold Storage"
  - "Security"
url: "/Crypto/Hardware-Wallets-Are-Not-a-False-Proposition"
---

The recent supply-chain compromise of Ledger devices (analyzed in [a companion piece](/Crypto/Security-Is-the-Ultimate-Luxury/)) has left a lot of people nervous — suddenly doubting the hardware wallet they trusted. That reaction is understandable. But it does not mean a hardware wallet is a false proposition.

To see why, we have to separate the *product* from the *idea*.

## A product, and a commodity

A hardware wallet from Ledger, OneKey, or any other vendor is, first, a **product** — something designed and built to meet a need — and second, a **commodity** — something that enters the market to be exchanged and sold. The two words describe the same object from different angles: "product" emphasizes function, "commodity" emphasizes the transaction.

Think of a car. As a product, its purpose is safe, efficient travel. As a commodity, it must be manufactured, priced, marketed, sold, and serviced. The value of the product is that it moves you safely; the nature of the commodity is that someone is trying to make a profit selling it.

A hardware wallet is no different. Vendors design and build devices around private-key storage, transaction signing, secure elements, firmware, and user experience, then push them through distribution channels to consumers. So the first thing to accept is that a hardware wallet, as a concrete commodity, inevitably carries the ordinary risks of any commodity: manufacturing defects, production slip-ups, reseller problems, supply-chain attacks. A good reputation built over years does not guarantee that every single unit is safe.

What made the Ledger incident so unsettling is precisely that it touched the easiest link to ignore: we assume we are buying a secure device from a famous maker, but in reality we are also trusting the *entire journey* from factory to doorstep.

That said, we should not "give up eating for fear of choking." One brand's defective product does not invalidate the whole concept. To understand the difference, we have to step up one level from the commodity and ask what problem a hardware wallet actually solves.

## The first principle: isolate the key

A hardware wallet is, first and foremost, a **security scheme**, and only secondarily a physical product.

Its first principle is simple to state: keep the private key (and the recovery phrase) isolated from any networked environment, so that the key and its recovery credentials can never be touched, read, copied, or transmitted by an unauthorized person or device during generation, storage, and signing.

The "private key" here means the key itself, the mnemonic used to recover the wallet, and the keys derived from that mnemonic. The mnemonic can regenerate the entire key hierarchy; in the wrong hands, an attacker can rebuild the wallet on another device and move the funds.

Why isolation? Because in a system like Bitcoin, the credential that actually controls the assets is the private key (mnemonic). The asset records do not live inside your hardware wallet — the device holds the keys that control them and uses those keys to sign transactions. Anyone who obtains a key strong enough to control the wallet can drain it from the other side of the planet, without ever touching your device or entering your room.

So the core value of a hardware wallet is to erect a security boundary: the online machine fetches information, builds the transaction, and broadcasts it; the offline environment holds the keys and performs the signing. Normally, the networked computer hands the unsigned transaction to the hardware wallet, the wallet signs it internally, and returns only the signature. Transaction data and signatures may leave the device; the private key must not.

That is the basic logic of a hardware wallet.

Knowing the first principle, however, does not let us ignore how a specific device implements it. Whether the isolation boundary truly exists, whether keys are generated and used only inside it, whether the firmware can be maliciously altered, whether what the screen shows matches what gets signed — all of that depends on concrete hardware design, software implementation, and security verification.

This is exactly why one hardware wallet having a security problem does *not* mean the concept has lost its value. (My own view, for reference.) If a device is tampered with during production or distribution so that the very mnemonic it was supposed to protect leaks out, that proves the device failed to achieve the security goal we asked of it. We should investigate the device, the manufacturing, the sales channel, and the verification mechanism — not conclude that every similar scheme is worthless because one implementation failed.

## Do you even need a dedicated device?

Since the core is key isolation, must you buy a purpose-built hardware wallet? Clearly not.

In principle, an old phone properly prepared — factory-reset, loaded with vetted wallet software, with all networking disabled — can serve as a cold wallet. So can a fully air-gapped computer, a specific single-board computer, or any device that can generate keys and sign in a trusted environment. You generate the mnemonic on that offline phone, ensure it never touches a networked device, then pass the transaction in via QR code or another safe channel, sign it, and hand the signature back to the online machine to broadcast.

In principle, this works — and complete implementations existed as far back as 2014. But there is a vital precondition: you must actually understand what you are doing.

An old phone does not become a safe cold wallet just because you turned off Wi-Fi and pulled the SIM. A phone is a general-purpose device: operating system, wireless modules, apps, system services, a thicket of complex software. You may not be able to confirm it was never infected, nor judge whether its firmware is trustworthy, nor fully master the key-generation, signing, and transfer process. A factory reset clears user data; it does not prove the entire software and hardware environment deserves your trust.

I have said before that a used iPhone can double as a hardware (cold) wallet, and that some phone secure enclaves now match the security grade of dedicated wallets. But here is the catch: even with networking fully off, some phones retain a fallback connection path — for instance, a "find my phone" feature that, strictly speaking, is not a network function but a backup protocol communicating with other devices. If an attacker reverse-engineers that, every precaution before it is wasted. For a used device, this deserves special attention.

And with AI models growing more capable by the day, which vendor would dare claim their device is *absolutely*, *never*, uncrackable?

A purpose-built hardware wallet cannot promise absolute safety either. But it can narrow the things you personally must get right — through a clear security boundary, a dedicated signing process, protected key storage, limited functionality, and an on-device confirmation screen. Some add secure elements, firmware verification, even tamper-responsive self-destruction. In short, a dedicated wallet offloads part of the complex security work onto a designed product, lowering the bar for ordinary users to achieve [self-custody](/Crypto/Self-Custody-Faith-Collapse-or-Rebirth/).

An old phone can be turned into a cold wallet, but you shoulder far more design, verification, and maintenance yourself. When you buy a dedicated wallet, you pay not just for the silicon but for the product design, R&D, software support, and security mechanisms that buy you convenience.

## Every choice has its own risk structure

Once you actually start comparing options, a reality emerges: each choice carries its own distinct risk structure.

- **Keep funds on an exchange** — effortless, but the keys are in someone else's hands. FTX's users learned this in a few days in November 2022: the platform's scale, its founder's celebrity, the backing of top-tier investors — none of it stopped the misappropriation of customer assets[1].
- **Use a phone hot wallet** — convenient, fine for small daily amounts, but the device is stuffed with networked apps. One clipped-board hijack, one mis-tapped approval, one poisoned app, and the balance can go to zero.
- **Buy a commercial hardware wallet** — a step up in security, but you ride the vendor's entire chain. As noted, a commodity always drags along its supply chain.
- **Use an open-source hardware wallet** — you can inspect more source, even compile it yourself, but open source is not automatically secure. (Coldcard: I suspect you're looking at me.)
- **Build your own cold wallet from an old phone** — saves the device cost and grants more autonomy, but every bit of verification and operation is on you.
- **Choose a model with a screen** — you can review address and amount before signing, but you still must judge whether what the screen shows is complete and trustworthy. **Bluetooth models** are more convenient yet add communication and software layers to evaluate. **Fully offline models** shrink the network surface but raise questions of firmware updates, device recovery, long-term maintenance, and signing process.

And even going fully offline does not make risk vanish. Devices fail. Mnemonics are lost. Backups burn or flood. Family members fumble. You yourself may one day forget a critical recovery step. Even brain wallets, paper wallets, steel plates, copper, silver, "money wallets"…

Security is never a single metric. It is about what an attacker can touch, what you are willing to trust, what you can verify, and whether you can maintain your setup over the long haul.

## Threat models scale with wealth

Here is the more important point: which option is "better" ultimately depends on the *person* and the setup they can actually execute.

The "good news" is we have many versions to "choose" from:

- **Exchange:** peace of mind, at the cost of keys in others' hands.
- **Phone hot wallet:** convenience, at the cost of a device full of networked apps.
- **Commercial hardware wallet:** a security step up, at the cost of riding the vendor's whole chain.
- **DIY old-phone cold wallet:** cheap and autonomous, at the cost of all verification resting on you — no bonus for getting it right, no one to catch you if you get it wrong.
- **Multisig:** one lost key doesn't drain the funds, at the cost of complex process and hard recovery; the more you scatter the keys, the higher the odds that one day you forget, lose contact, or bungle the process.

Looking at the historical record, an attacker's default strategy is to go around. Breaching a physically isolated device costs far more than sending ten thousand phishing emails.

So the first principle of hardware wallets still stands — it just protects a narrower boundary than many assume. It protects the key itself; everything outside the key still depends on your own judgment.

And then there is the increasingly discussed **"wrench attack."** Its essence: the size of your holdings rewrites your threat model. User data leaked back in 2020 was recycled by scammers for years. In January 2025, Ledger co-founder David Balland was kidnapped in France, the kidnappers demanding a crypto ransom; that same year French police charged 25 suspects across a wave of such abductions targeting crypto people and their families[2]. When your position grows large enough, the attacker walks from behind the screen to in front of you.

That is why flaunting holdings, withdrawal records, or address balances is effectively pre-pricing yourself. Splitting funds, staying low-key, and using multisig only start to matter at that level.

## Three questions before you choose

Before picking a scheme, answer three questions:

1. **Capability** — Can you verify transaction parameters line by line? Can you build and maintain an offline environment? Can you read a signing tool's error messages?
2. **Awareness** — Can you spot phishing? Do you know what unlimited token approval means? Do you understand that official support will never DM you for your mnemonic?
3. **Discipline** — Will you run a recovery drill once a year? Can you sustain a process for five years? After moving, changing phones, or losing a device, can you still find your backups?

Stack up those three answers and the right scheme reveals itself. No one else's answer substitutes for yours. The KOLs' pitches exist to earn referral fees; the vendors' marketing carries their own agenda — as we saw when every vendor rushed to tweet about its own product after the Ledger incident. And the emotions swirling through group chats are just that: emotions. Only you know where your own line of capability, awareness, and discipline actually falls.

## There is no absolute security

This leads to the ultimate reflection on security: there is no absolute security in this world, so never blindly chase it.

Many newcomers to crypto carry a perfectionist streak. They want a flawless scheme that parks assets in a fortress no god could crack. To reach that absolute safety they accumulate ever more complex gear, devise recovery mechanisms too convoluted to remember, and live in constant anxiety. That state has already drifted from the point of managing assets — the essence of investing and asset management is to make life better, not to torture yourself with endless worry.

No matter how elaborate the security system, in the end *you* are the backstop — your memory and your operational ability. Protection beyond your capacity will turn around and bite you.

In the real world, risk can never be utterly eliminated. What we can do is not chase a phantom 100% safety, but build the most cost-effective defense within a controllable budget. Understand the risk, assess yourself, match your capacity, and bear the cost — that is the eternal rule for surviving in crypto.

A hardware wallet was never a false proposition. It is merely one tool we use against risk. And how a tool is used always depends on the person holding it.

Verify. Don't trust.

## References

- **[1]** FTX collapsed in November 2022 after customer withdrawals exposed an $8B hole and the misappropriation of customer funds — [Wikipedia: Bankruptcy of FTX](https://en.wikipedia.org/wiki/Bankruptcy_of_FTX)
- **[2]** Ledger co-founder David Balland was kidnapped in France in January 2025; French authorities later charged 25 suspects in a wave of crypto-targeted abductions — [Le Monde](https://www.lemonde.fr/en/pixels/article/2025/01/25/seven-arrested-in-france-for-kidnapping-and-torture-of-crypto-co-founder_6737412_13.html)
