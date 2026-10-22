---
title: "Bitcoin's Quantum Dilemma: Who Decides Satoshi's Exposed Coins?"
date: "2026-10-20T17:29:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Bitcoin"
  - "Quantum"
  - "Satoshi"
  - "Security"
  - "Post-Quantum"
url: "/Crypto/Bitcoins-Quantum-Dilemma-Who-Decides-Satoshis-Coins"
---

On Tuesday, Bitcoin nudged lower around the $81k line, the tape as grindy as ever. Away from the price action, the quantum-computing front saw fresh movement — the latest turn in a story we have followed about <a href="/Crypto/The-Quantum-Sword-Honed-by-AI/">the quantum threat to Bitcoin's signatures</a>. On October 16, nine blockchain companies announced the formation of the Quantum Alliance, a body meant to set a set of quantum-safety testing standards for blockchains, wallets, and infrastructure.

The alliance's positioning is clear: unable to change Bitcoin's code, it will instead build a yardstick outside Bitcoin itself, to assess how quantum-ready each part of the ecosystem is. That same reluctance to touch Bitcoin's scripting surface is exactly what keeps the protocol's application layer thin — the theme we pick up in our essay on [Jack Dorsey and the "digital gold" debate](/Crypto/Jack-Dorsey-If-Bitcoin-Ends-Up-Just-Digital-Gold-It-Has-Failed/). The member roster — Quantus, American Fortress, Intmax, Keystone, Midnight Foundation, Postquant Labs, Abelian, The Vault, and Hacken — is a clean slate of public chains, wallets, and security vendors; no Bitcoin Core developer appears on the list [1]. Modeled on the IETF, the alliance splits into four working groups: blockchain migration, post-quantum zero-knowledge systems, wallet security, and cross-chain compatibility.

By their estimate, some [6.04 million BTC — about 30% of total supply — already have their public keys exposed on-chain](/Crypto/Bitcoin-Quantum-Risk-6-Million-BTC-Exposed/) and could, in theory, have their private keys reverse-engineered by a sufficiently powerful quantum computer. But an exposed public key is not the same as a bare-public-key address. Part comes from early pay-to-public-key (P2PK) outputs, where the public key is written straight into the locking script; the rest comes from addresses like P2PKH that, once they have been spent, leave the public key on-chain alongside the signature. Of that total, roughly 1.0–1.1 million BTC are attributed to Satoshi, by the Patoshi-pattern accounting [2].

How should these troublesome coins be handled? In particular, if they have fallen silent — the owner gone or the private key lost, unable to move the coins to a safe address — then what?

The alliance is not of one mind on the answer. One camp wants to move the coins out and re-house them in a quantum-resistant way; the other worries that, the moment the protocol gains the ability to dispose of any dormant coin, it opens a precedent that breaks property rights and neutrality alike. Move or freeze — a question argued in academia for over a year — has now been placed on the industry's table, unchanged.

The proposals on the table are, counted up, still the same unsettled ideas. BIP-361 has sat in the official repository for more than half a year: status Draft, type Informational, filed February 11, 2026 [3]. Its design runs in two steps — first, forbid further transfers to old, exposed-public-key addresses, herding new funds behind the quantum-resistant door; then, five years on, by a widely publicized flag day, bring the old signatures under a so-called quantum-safe rescue protocol. The word "freeze" never appears on the page, but the effect is not far from it.

Hourglass V2 takes another path — rate-limiting. At most one P2PK spend per block, with net outflow no greater than one bitcoin, which works out to about 144 BTC a day. The proposal still has no formal BIP number; it circulates only on the Delving Bitcoin forum and the bitcoindev mailing list [4]. Its aim is simply to slow things down — imperfect, and with little consensus behind it.

The third road comes from Paradigm's Dan Robinson, who published PACT on May 1, 2026 [5]. A holder can, today, quietly create a timestamp that proves they knew the private key before any quantum computer existed; tomorrow the protocol could accept that zero-knowledge proof as an alternative spending path for the old address. The single most important move in the whole design is that it devotes a section of its own, titled precisely "The Satoshi Problem."

The coins suspected of belonging to Satoshi are exactly the most special class within this exposed-public-key group. P2PK writes the public key straight into the locking script, public from the day it went on-chain; that era had no BIP-32 parent-key derivation, no BIP-39 mnemonic, not even the P2PKH hash-protected public-key address. The premise of zero-knowledge rescue is that you can prove you know something others do not — which requires the address to have been derived from a mnemonic. P2PK has no such thing. The authors of BIP-361 concede in the document itself that they do not currently believe a rescue protocol can be constructed for P2PK UTXOs, because no known asymmetry of knowledge exists [3].

PACT shifts the asymmetry from the seed to time. A quantum attacker can compute the private key but cannot forge a timestamp anchored to the chain long before. It also gives silence its first cost-based solution: no need to move publicly, no need to reveal identity — simply leave proof behind, in advance, while no one is watching. This is the most likely path that could still work for Satoshi, but it also depends on Satoshi still being alive and able to sign a proof ahead of time.

This is not a simple problem. The whole industry is still thinking, still debating fiercely. We must not open the door to confiscatory freezing — that trades Bitcoin's neutrality for a sense of security that will not last, a trade we have argued elsewhere is exactly what makes a <a href="/Crypto/Why-Blockchain-Matters-More-as-AI-Gets-More-Powerful/">decentralized blockchain the more valuable as centralized power grows</a>. But lying flat may be no answer either: the 6.04 million exposed-public-key coins sit there, and the quantum-computing schedule tightens year by year. Even if some of it is FUD, even if quantum computing never manages to break Bitcoin, the awareness to prepare ahead of time is always indispensable.

Nine companies forming an alliance will not change or forge consensus overnight. But at least, from now on, an organization is focused on the subject. The quantum computer is not built yet, but the table where someone speaks for Satoshi is already set. One even wonders: if several institutions of some credibility joined to create a multisig address, and on the eve of a quantum breakthrough moved the coins from early P2PK addresses — Satoshi's included — under the guise of protective transfer, later letting owners reclaim them with some proof, might that be the sort of solution this alliance produces?

If Satoshi is dead, or unwilling to expose their identity, for whatever reason unwilling to reclaim, then those coins would remain in the alliance's custody forever. (Of course, this is purely speculation.)

## References

- **[1]** Crypto Briefing — *Nine blockchain groups unite to set open standards for post-quantum readiness.* The Quantum Alliance (Quantus, American Fortress, Intmax, Keystone, Midnight Foundation, Postquant Labs, Abelian, The Vault, Hacken), launched Oct 15–16, 2026, IETF-style, four working groups. https://cryptobriefing.com/?p=395600
- **[2]** KuCoin — *Bitcoin's Satoshi Nakamoto Coins May Be Frozen to Prevent Quantum Theft.* Patoshi-pattern estimate of ~1.1M BTC; BIP-361 notes >34% of supply had an exposed public key as of March 1, 2026. https://www.kucoin.com/news/flash/bitcoin-s-satoshi-nakamoto-coins-may-be-frozen-to-prevent-quantum-theft
- **[3]** BIP-361 — *Post Quantum Migration and Legacy Signature Sunset* (Draft, Informational, assigned 2026-02-11; authors include Jameson Lopp). Two-phase sunset plus an optional ZK seed-phrase rescue; authors concede no known rescue for P2PK UTXOs. https://bips.dev/361/
- **[4]** Delving Bitcoin — *Hourglass V2 Update.* Rate-limits P2PK spends to one per block, net ≤1 BTC (~144 BTC/day), no formal BIP number yet. https://delvingbitcoin.org/t/hourglass-v2-update/2246
- **[5]** The Block — *Paradigm researcher proposes timestamp 'escape hatch' to protect Satoshi-era bitcoin from quantum threats.* Dan Robinson's PACT (Provable Address-Control Timestamps), published May 1, 2026, with a section titled "The Satoshi Problem." https://www.theblock.co/post/399738/paradigm-researcher-timestamp-escape-hatch-satoshi-era-bitcoin-quantum
