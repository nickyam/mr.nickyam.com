---
title: "The Quantum Mine: A Game-Theoretic Approach to the Quantum Threat"
date: "2026-11-06T16:24:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Bitcoin"
  - "Quantum Computing"
  - "Game Theory"
url: "/Crypto/The-Quantum-Mine-A-Game-Theoretic-Approach-to-Quantum-Threat"
---

Overnight, Bitcoin failed to hold above $80k and fell back. A new term surfaced in the developer mailing list.

On November 4, developer Cory Fields proposed a mechanism called the "quantum mine" on the bitcoin-dev mailing list[1]. He works at the MIT Digital Currency Initiative and is also a Bitcoin Core developer. The proposal has not yet been written up as a formal improvement proposal, and he himself says it is only a thought experiment.

The mechanism itself is not hard to understand. Anyone who wants to claim the BTC in a vulnerable address (such as early P2PK addresses, or addresses that have exposed their public key) must first lock an equal amount of BTC from a quantum-safe wallet as collateral. The coins in the target address and this collateral are locked together, for example for thirty days. During this waiting period, if the address's owner can produce a hidden proof of ownership, they can reclaim their own coins and, along the way, take the claimant's collateral as well.

What is interesting about this idea is that it thinks in terms of game theory rather than cryptography.

For the past few years, the main thread of discussion around the quantum threat has been migration. Schemes like P2QRH would change the signature algorithm; a soft fork would require every node and wallet on the network to upgrade; all holders would have to move their coins from old addresses to new ones. This path is technically sound; the hard part is mobilization. Millions of addresses have been dormant for years — their owners may have lost the private key, may have passed away, or may simply not know any of this is happening.

The quantum mine changes direction. Instead of mobilizing holders to migrate, it puts the claimant in jeopardy. Want to steal $100 million in coins? Put up $100 million first. Steal successfully, gain $100 million; get caught, lose $100 million. By changing the odds this way, a rational actor will not move.

It is a genuinely elegant idea. But before going further, one point must be added: the mine has to be planted by the holder themselves; the protocol will not do it automatically.

The planting happens before the so-called Q-day (the day quantum computing breaks private keys). The holder needs to use a new quantum-safe address to create a very small output that hides a commitment. The content of the commitment is simple to state: it proves that, before a quantum computer could compute the private key, I already held the private key to this old address. The commitment itself does not reveal the private key; it only fixes, in advance, on-chain, the fact that I knew it, to be revealed and verified later when needed[2].

Why must it be before Q-day? Because after Q-day, a quantum attacker could in theory compute the same private key. Looking only at the signature, the chain cannot tell whether someone is the original owner or someone who computed the key later. Only a commitment planted before Q-day separates the person who knew first from the person who computed it later.

When Q-day arrives, the new validation rule activates. To then move coins from an old address, one must put up equal collateral and also take a time-locked alternative spending path. The developer's example goes like this: Alice places 1 BTC in an old output, 1 BTC in a quantum-safe wallet, and additionally plants a tiny mine. A claimant comes to move that 1 BTC and must put up another 1 BTC themselves; the two are locked together for about thirty days. During those thirty days, Alice reveals the commitment (detonates the mine), reclaims her coins, and takes the claimant's collateral along the way.

The claimant cannot tell in advance which addresses are mined. This is the key to the whole design: every attempt requires putting up equal principal first, and whether you hit a mine is pure luck. Hit one, and the principal is gone.

But at this point a piece is still missing: how does the owner themselves claim?

The developer's mechanism is designed to catch thieves. Under the existing framework, for the owner to migrate proactively, they would also have to go through that collateral process. In his email he acknowledges the need for an execution rule that pushes the collateral burden onto the claimant while leaving an honest migrator a path that does not require equal collateral. He did not write that rule.

Thinking further along this question, there may in fact be a solution. The commitment can be signed with a quantum-safe address; a claimant can compute the old private key but cannot forge the commitment itself. Add the timestamp evidence the commitment carries, proving which day it was planted. With these two things, the owner presenting the commitment should be able to claim the coins directly, without putting up equal collateral.

Even better, the owner has another option: do not rush to claim; wait for someone to step on it. The claimant puts up equal principal, locked into the waiting period; the owner then reveals the commitment and takes both their own coins and the claimant's collateral. The mine turns from passive defense into active ambush.

From this, the waiting period also seems worth lengthening. A thirty-day lock allows twelve rounds of attempts per year; if locked for a year, only one round per year. The single-attempt odds do not change, but the number of addresses covered differs by an order of magnitude. Without enough empty addresses, you cannot assemble a profitable sample. Lengthening the lock weakens the coverage of probing, and the speed of capital turnover.

A well-funded claimant can use parallel collateral to buy time — posting many attempts at once, at the cost of several times the consumption. So it deters small and mid-sized claimants, but not unlimited firepower. Here Bitcoin's absolute scarcity becomes an advantage: no one has unlimited firepower.

With this small modification, its difference from BIP-361 (draft) becomes clear. BIP-361 is deadline migration — freeze on expiry, the protocol makes the decision for everyone; whereas the quantum mine idea leaves a collateral exit, so someone who has not proven in time can still collateralize for a year to claim their coins, while using mine-strikes and capital occupation to deter claim-jumping. Its treatment of property rights is far gentler than a one-size-fits-all freeze.

Of course, for those coins that have truly lost their owner, there is still no solution. The mine only helps those who still hold the private key; coins whose private key is already lost — including Satoshi's early holdings — have no owner who can come forward to reveal a commitment.

Either path shares roughly the same premise: the owner must act once before Q-day. After Q-day, what can be proven reduces to mere knowledge of the private key, and by then knowing the private key no longer equals being the true owner. The only still-valid proof is that I knew before Q-day. But that proof can only be left before then; timestamps do not flow backward. Those who took no action beforehand have no remedy afterward.

The line of extended thinking above follows the developer's reasoning further and goes beyond his original proposal. The inspiration of this mine-planting idea lies not in some detail, but in its direction. For years, discussion of the quantum threat has revolved almost entirely around cryptography — changing signature algorithms, modifying address formats, mandating migration. This developer shifted the focus to game theory, making the cost of attack itself the object of design.

There may be better ways to go down this direction. These reflections are offered in the hope of attracting broader discussion: beyond asking people to migrate, beyond freezing coins, beyond collateral, is there a better solution?

## References

- **[1]** Cory Fields, "quantum mine" proposal on the bitcoin-dev mailing list, November 4, 2026. Described by the author as a thought experiment rather than a formal Bitcoin Improvement Proposal; Fields is a Bitcoin Core developer at the MIT Digital Currency Initiative.
- **[2]** The commitment scheme: a hidden on-chain pre-commitment that proves pre-Q-day knowledge of an old address's private key without revealing the key itself, to be verified later when needed.
