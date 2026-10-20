---
title: "Security Is the Ultimate Luxury"
date: "2026-10-12T13:03:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Hardware Wallet"
  - "Cold Storage"
  - "Supply Chain"
  - "Self-Custody"
url: "/Crypto/Security-Is-the-Ultimate-Luxury"
---

Last Friday (Oct 9), BTC quietly retested its 50-day line (around $80.7k), then, after a two-day weekend, climbed back to $83k–$84k. But what sent a chill down the market's spine was not the price action. It was a supply-chain attack on [Ledger hardware wallets](/Crypto/Hardware-Wallets-Are-Not-a-False-Proposition/) that, by some accounts, drained close to $100 million.

A Ledger unit shipped from Malaysia, when opened, was found to contain a tiny board where the screen's padding should have been — a board that had no business being there. On a fingernail-sized piece of silicon sat a full mobile-communications stack: an LTE module, an antenna, an eSIM, plus a microcontroller wired into the device's SPI bus. It cannot crack your password, but it quietly watches the screen, memorizes the 24 words you jot down during setup, and beams them out[1].

Security researchers' reconstruction: the seed phrase is generated inside the secure element and shown on screen for you to copy. The malicious module lifts the displayed content straight off the screen's data lines. The secure element can stop the private key from being read; it cannot stop the screen from showing what it shows[1]. Subsequently, the reseller CryptoBilis was revealed to have quietly changed hands back in March[2]; and Ledger itself confirmed that one user's device contained an unauthorized hardware implant[3].

So the nature of the incident is clear. What got breached was not the elliptic-curve algorithm. It was the path between the factory and your hands. A textbook supply-chain attack. Most people had never heard the term, and this was the first time many had seen an attack this high-tech.

By technical definition, a hardware wallet is classed as "cold" precisely because it never touches the network.

But hackers have ways to make your hardware wallet quietly get online.

Strictly speaking, then, a hardware wallet cannot be 100% guaranteed "cold" across its lifecycle. Borrowing a term from quantum physics: a hardware wallet is Schrödinger's cold. Only at the moment you get robbed does the wavefunction collapse into a definite, alive-or-dead outcome.

Seen from this quantum — or probabilistic — angle, the various "cold storage" approaches differ in degree of coldness. Roughly ranked from coldest to not-so-cold:

- **Coldest:** paper wallets (and variants — steel seed plates, brain wallets)
- **Colder:** your own air-gapped device (a PC with its network card pulled, a phone with the SIM removed, Wi-Fi off, airplane mode on)
- **Least cold:** a purchased hardware-wallet product

In March 2025, an analysis examined why a so-called "cold wallet" holding over a billion dollars at an exchange got cleaned out. The lesson: for a smart-contract wallet, a private key that never touches the network does not equal safe assets, because real control lives in the on-chain contract, which is always online. Strictly, then, the test for "cold" is not "the private key never touches the network" but "control never touches the network, never touches electricity."

Earlier, in June 2024, another piece asked where one can buy a cold wallet — and the answer was unexpected: a stationery store. A pen and a notebook. Generate the key offline, hand-copy it twice, verify the address, then lock it in a safe. Clumsy, slow, undignified — yet with one advantage no hardware wallet can offer: no supply chain. No factory, no logistics, no reseller, no one who could tamper with the chain in advance.

Looking back, the value of a hardware wallet lies in convenience and engineering reliability. A dedicated chip and audited firmware are genuinely easier to use than a piece of paper, especially for assets you touch often. Its weakness is exactly there. For convenience's sake, it must pass through an entire chain you cannot personally supervise; compromise any single link and the device is no longer safe.

There is an even simpler, almost insultingly simple supply-chain attack: a fourth-party seller prints a beautiful seed-phrase card, pre-loads it with a chosen phrase, and slips it into the box. The user receives the device and, without suspicion, imports the preset phrase per the "instructions." The reader surely sees at once how the attacker then walks off with the funds. If you don't, you should study crypto basics before touching a hardware wallet.

Which is why the advice hammered home for beginners is: never, ever buy a hardware wallet from unofficial e-commerce channels. After this Ledger episode, even an "official authorized reseller" has proven to be a weak link.

In June 2025, another case told of someone who bought the right device but photographed the seed phrase on their phone, or lazily stored it in the cloud. The device was fine; the human failed.

This is not to write off hardware wallets, nor to deny their usefulness. One can own a Ledger and use it. But the most critical holdings should not sit on it. For accumulation and long-term holding, a colder method of sealing is worth it.

A hardware wallet's convenience shows up most when you use it often. But the moment you use it, it connects. Through a USB cable to a networked computer, or Bluetooth to a networked phone — but a two-hop connection is still a connection.

So a hardware wallet's cold is not always-cold, but sometimes-cold, sometimes-not.

The industry has even minted a concept between hot and cold, calling it the "warm wallet."

Used properly, a Ledger simply separates the [signing key](/Crypto/Self-Custody-Faith-Collapse-or-Rebirth/) from a directly-networked device (the PC), adding a sliver of security.

At first principles, a hardware wallet is a commercial product. The manufacturer produces for profit. Under that relationship, the incentive to ship new features and new products often overshadows the incentive to be maximally conservative and guard security above all.

Take Ledger: the simplest, cheapest old-model Ledger — one that requires a physical USB cable — is the sound choice here; fancy Bluetooth and luxury features only add risk points for no good reason.

A product is a system. From the plainest quality-control principle, the more components, the more functions, the higher the luxury, the higher the probability something goes wrong. Especially when the maker's attention is on splashy, marketable features, it tends to shortchange the most basic life-and-death security functions — creating a strange security paradox:

**The more luxurious, the greater the security risk.**

Perhaps every user should keep Occam's-razor thinking close: do not multiply entities beyond necessity. Every flashy feature added is likely a risk point. Even if it isn't itself a risk, it can blind you to real ones elsewhere by diverting attention from security.

Nature follows the way of "heaven and earth are unkind" — its cruelty lies in never teaching, only selecting. When a person's understanding cannot match their wealth, their money flows to someone else's pocket. It is the same cognition gap we examine when asking how ordinary people should approach the crypto ecosystem as AI and centralized finance expand; we take up that question <a href="/Crypto/Why-Blockchain-Matters-More-as-AI-Gets-More-Powerful/">in this essay</a>.

Security is the ultimate luxury.

## References

- **[1]** Mark Karpelès' teardown of a Malaysia-sourced Ledger showing a hidden board (microcontroller, antenna, LTE chip, eSIM) on the screen's SPI line that captures the seed phrase as it is displayed — [TheCryptoDesk](https://thecryptodesk.com/news/mark-karpeles-finds-hidden-spy-chip-inside-sealed-ledger-hardware-wallet)
- **[2]** CryptoBilis, the Southeast Asian Ledger reseller, changed ownership in March 2026 (100% held by a Heilongjiang-registered individual since Aug 3) — [The BlockBeats](https://en.theblockbeats.news/flash/371090)
- **[3]** Ledger confirmed at least one affected device contained an "unauthorized hardware implant"; third-party researchers estimate losses of $86M–$93M (unverified) — [Help Net Security](https://www.helpnetsecurity.com/2026/10/12/ledger-wallets-compromised-via-hardware-implant/)
