---
title: "Bitcoin Quantum Risk: 6 Million BTC Exposed — Where Does It Come From?"
date: "2026-10-22T09:45:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Bitcoin"
  - "Quantum"
  - "Security"
  - "Public Keys"
url: "/Crypto/Bitcoin-Quantum-Risk-6-Million-BTC-Exposed"
---

Recent industry research has zeroed in on a new security question for Bitcoin: which coins are actually exposed to quantum risk right now, in their current holding state? The core test is whether the public key needed to spend a coin has already been revealed on-chain. By that measure, roughly **6.04 million BTC — 30.2% of total issuance — currently sit behind public keys that are already visible on-chain** [1]. The remaining 13.99 million BTC (69.8%) keep their public keys hidden while dormant, and are not exposed under this model. (A subsequent update from the same researcher on October 8 later revised the exposed figure to 6.26 million BTC, or 31.2% of supply [2].)

We can split the risk into two kinds. The first is **structural risk**: the script type itself leaks the public key on-chain. The second is **operational risk**: coins that were once protected but whose public keys have since been exposed through address reuse, partial spends, or custody practices.

![Bitcoin supply by quantum safety (share): safe 69.9%, structurally unsafe 9.6%, operationally unsafe 20.6%. Source: Glassnode.](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8pJq2XEH6KMvpzJ3Ac39FlZWc3qGbQACzRFrGxelyFZR6ta_UVFmcAEAAwIAA3kAAz0E.png)

*Bitcoin supply by quantum safety (share). Safe: 69.9%; structurally unsafe: 9.6%; operationally unsafe: 20.6%. Source: Glassnode.*

Of the total, 1.92 million BTC (9.6% of issuance) carry structural risk and 4.12 million BTC (20.6%) carry operational risk. Exchange custody alone accounts for about 1.63 million BTC — a reminder that wallet hygiene and custody design matter as much as protocol design in limiting public-key exposure.

This analysis takes no position on when a practical quantum attack might arrive, and makes no judgment about the security or solvency of any custodian. It only quantifies the current state of public-key exposure, separating permanently high-risk coins from those whose risk can be reduced with better wallet and custody practices. Read it as a measured exposure statistic, not a countdown — a distinction we explored in our piece on [shattering the quantum FUD](/Crypto/Quantum-FUD-Shattered-Bitcoin-Safe/).

## Public-key exposure, in plain terms

A bitcoin balance is controlled by a private key; the public key lets the network verify that a signature came from that private key. Under classical cryptography, a public key alone cannot be reversed into a private key, so a hidden public key is enough to keep coins safe.

The quantum threat works differently. A cryptographically relevant quantum computer could run Shor's algorithm to derive a private key from a known public key — the core worry we have tracked in our coverage of [the quantum sword, honed by AI](/Crypto/The-Quantum-Sword-Honed-by-AI/). That turns the on-chain question into a simple one:

- If the public key is already public, the coins are exposed. An attacker does not need to wait for the owner to move them — the public key is already available.
- If the public key is not visible on-chain, the coins are not exposed under this static storage model.

The focus here is on **dormant** balances: coins sitting still while their associated public keys have already leaked. That is different from transfer-time exposure, where a public key is only revealed when a transaction is broadcast and confirmed — a settlement-window risk rather than a stock of measurable risk. When a coin is called "safe" in this article, it means only that its public key has not been exposed while at rest — not that it is immune to every future quantum attack model.

## Structural exposure: unsafe by design

These coins are exposed because of their address script format, regardless of how carefully the owner uses their wallet. The category covers Satoshi-era P2PK addresses, legacy multisig P2MS addresses, and today's mainstream Taproot addresses. The vintages and use cases differ, but the common trait is the same: the public key — or an equivalent — is published on-chain from the start. As long as the coins are unspent, they are potential targets.

We currently classify 1.92 million BTC (9.6% of issuance) as structurally at risk, in three distinct cohorts:

![Structural risk cohorts: Satoshi 1.10M BTC (5.5% of supply), Satoshi-era 0.62M BTC (3.1%), Taproot 0.20M BTC (1.0%).](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8oxq2XDAKlz0he9iYJToP1hZqFB2IwACxxFrGxelyFZaA0Hg2n7EtAEAAwIAA3kAAz0E.png)

*Structural risk cohorts: Satoshi 1.10M BTC (5.5% of supply), Satoshi-era 0.62M BTC (3.1%), Taproot 0.20M BTC (1.0%).*

![Structurally unsafe Bitcoin by source: Satoshi 5.5%, other Satoshi-era 3.1%, Taproot 1.0%. Source: Glassnode.](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8o1q2XDFZBMFU5_9i6WSzNeZchvwHAACyBFrGxelyFb07U5A7DRlGgEAAwIAA3kAAz0E.png)

*Structurally unsafe Bitcoin by source. Source: Glassnode.*

**Satoshi and early-block coins** are permanently exposed. If they are lost or their holders are silent, there is essentially no way to migrate them to safe addresses — unless the whole network reaches consensus on a protocol-level fix, they will stay exposed to quantum risk indefinitely. What should happen to this stock, and who gets to decide, is precisely the question at the heart of [Bitcoin's quantum dilemma](/Crypto/Bitcoins-Quantum-Dilemma-Who-Decides-Satoshis-Coins/).

**Taproot addresses** are a different story. The script has real advantages — strong privacy, efficient transfers, flexible smart contracts — and is not a design flaw. But from a public-key exposure standpoint, Taproot publishes its key directly, leaving dormant balances exposed.

The industry's proposed answer is BIP-360's P2MR output type [3], which keeps Taproot's functionality while removing the high-risk key-path spend. It cannot, however, auto-migrate existing Taproot balances, and it is not a complete post-quantum solution on its own [4].

In short, of the 1.92 million structurally exposed coins, one part is nearly impossible to migrate, while the rest can be progressively de-risked with new protocols and standards.

## Operational exposure: unsafe by habit

These addresses are born with privacy protection — they do not leak public keys at rest. Exposure only happens when the owner's own actions reveal the key mid-spend, leaving the remaining balance unprotected.

This is the address-reuse problem. Output types like P2PKH, P2SH, P2WPKH and P2WSH hide the public key behind a hash while the coins sit still. But once a spend reveals the public key, every balance tied to that key — present and future — loses the protection.

Operational exposure is now the dominant source of Bitcoin's quantum risk: 4.12 million BTC, 2.1x the structurally exposed stock. It confirms that most of Bitcoin's quantum exposure today is not a legacy scripting problem but a key-management and address-hygiene problem.

![Operationally unsafe BTC supply: other 12.3% of total supply, exchanges 8.3%. Source: Glassnode.](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8o5q2XDKH7xIZEWfL5dMD20O1cGNbwACyRFrGxelyFZ5RvVn_ZSgyQEAAwIAA3kAAz0E.png)

*Operationally unsafe BTC supply: other 12.3% of total supply, exchanges 8.3%. Source: Glassnode.*

Within the operationally exposed stock, exchange custody looms large: about 1.66 million BTC, roughly 40% of all operationally unsafe balances. The data also shows a stark split — about half of labeled exchange holdings are exposed, versus under 30% for non-exchange holdings.

![BTC exchange supply by platform, with operationally unsafe shares marked. Source: Glassnode.](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8o9q2XDX9OQISbvwlDqb9V1HKB0edAACyhFrGxelyFadwyKjXtZInwEAAwIAA3kAAz0E.png)

*BTC exchange supply by platform, with the operationally unsafe share of each balance hatched. Source: Glassnode.*

## The custodian spectrum

Exposure varies enormously across institutions. Some custodians run relatively clean address books; others hold a large share of their balances in addresses with known public keys.

![Operationally unsafe Bitcoin by entity: exposure ranges from 0% for sovereign treasuries to 100% for several custodians. Source: Glassnode.](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8pBq2XDgKRsnoWZ_Ma80MXSWkIRhVQACyxFrGxelyFaxfDJkSPmxTAEAAwIAA3kAAz0E.png)

*Operationally unsafe Bitcoin by entity. Source: Glassnode.*

- **Low risk:** Coinbase has only ~5% of custodial assets with exposed public keys; sovereign treasuries (US, UK, El Salvador) show 0% exposure.
- **Medium risk:** Fidelity and Cash App around 2%; Grayscale around 50%.
- **High risk:** Binance 85%; Bitfinex 100%; Robinhood and WisdomTree fully exposed.

*Note: these figures reflect on-chain custody traces only. They are not a risk rating, a solvency judgment, or a statement about any institution's safety.*

Over the long run, governments have kept 99%+ of their holdings safe, while exchanges — with high fund turnover and complex wallet architecture — have seen their safe share slide from 55% in 2018 to about 45% today. The encouraging part: this is the most fixable category. Basic discipline — never reusing addresses, promptly sweeping change to fresh addresses — can shrink the exposed stock quickly.

![Operationally safe share by entity type: exchanges 44.8%, governments 99.7%, other 85.2%. Source: Glassnode.](https://yun.nickyam.com/file/AgACAgUAAyEGAASS2zT1AAEB8pFq2XDo774T_JGFueZ4M5N8zeQFUgACzBFrGxelyFbIukpBFtFHLQEAAwIAA3kAAz0E.png)

*Operationally safe share by entity type: exchanges 44.8%, governments 99.7%, other 85.2%. Source: Glassnode.*

## The takeaway

Bitcoin's quantum risk splits into categories with very different implications.

**Structural risk:** legacy coins are extremely hard to migrate; new protocols like P2MR can progressively de-risk modern Taproot addresses.

**Operational risk:** larger in size, but far more controllable — and the exchange-held stock is large enough that coordinated migration is realistic.

The broader lesson: quantum safety is not only a protocol-upgrade story. A large share of the exposed stock could be reduced today with ordinary operational discipline. For exchanges and professional custodians, disciplined address use, better reserve-address design, fewer key reuses, and a concrete migration plan are not distant ideals — they are practical, available-now ways to shrink quantum risk.

## References

- **[1]** ForkLog — *Glassnode Assesses Bitcoin with Exposed Public Keys*: the 6.04M BTC / 30.2% breakdown, the 1.92M structural / 4.12M operational split, and attribution to Glassnode co-founder Rafael Schultze-Kraft. https://forklog.com/en/glassnode-assesses-bitcoin-with-exposed-public-keys/
- **[2]** CoinAlertNews — *Glassnode Co-Founder Reveals 31% of Bitcoin Supply Behind Exposed Public Keys* (Oct 8, 2026): the updated 6.26M / 31.2% figure, exchange-level exposure (Coinbase 10%, Binance 83%, Bitfinex 100%), Fidelity 2%, Grayscale 49%, Revolut 99%, Robinhood 100%, and zero exposure for US, UK and El Salvador government holdings. https://coinalertnews.com/news/2026/10/08/bitcoin-exposed-public-keys-glassnode
- **[3]** BIP-360 — *Pay-to-Merkle-Root (P2MR)* (Hunter Beast, Ethan Heilman, Isabel Foxen Duke; draft): P2TR-like functionality with the quantum-vulnerable key-path spend removed. http://bip360.org/bip360.html
- **[4]** Lamarr Labs Field Guide — *Post-Quantum Blockchains*: context on BIP-360 vs BIP-361 (post-quantum migration and legacy signature sunset) and the long- vs short-exposure distinction. https://fieldguide.lamarrlabs.com/Post-Quantum-Blockchains
