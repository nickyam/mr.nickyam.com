---
title: "Shattering the Quantum FUD: Why Bitcoin's Cryptography Won't Crack Anytime Soon"
date: "2026-10-19T11:51:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Bitcoin"
  - "Quantum Computing"
  - "Cryptography"
  - "Security"
url: "/Crypto/Quantum-FUD-Shattered-Bitcoin-Safe"
---

Every few months the same panic returns. This time it was reignited by an interview clip in which Justin Sun argued that quantum computing and AI breakthroughs are reasons to be bearish on Bitcoin. Social feeds lit up with "quantum panic" all over again. Some were terrified, convinced the countdown to cracking Bitcoin's private keys had already begun, with talk of it happening within one to one and a half years. On Monday, however, Bitcoin was just grinding along above $80,000 — calm, with no sign of the panic the narrative promised.

This kind of fear, uncertainty, and doubt (FUD) shows up like clockwork, and almost every iteration stems from the same habit of thinking: linearly extrapolating a single scientific breakthrough. Google's Willow chip makes progress, and someone immediately treats it as a countdown timer for breaking Bitcoin. But quantum computing is bound by brutally complex physical engineering — it has never been a smooth exponential curve upward.

## What Willow actually is

Start with Willow itself. It currently has 105 physical qubits, and paired with a technique called *magic state cultivation* it reduced the error rate by roughly 40x, reaching a logical fidelity of 99.99% [1]. In the field of error correction, that is genuine, hard-won progress. It proves that error-correcting codes can correct their way to correctness — larger code distances mean logical error rates fall exponentially.

But calling the break "right around the corner" is a bait-and-switch. Going from a hundred-odd excellent physical qubits to the millions of *logical* qubits needed to break RSA or ECDSA spans several generations of hardware architecture. Google's own paper estimates that breaking RSA still requires fewer than a million physical qubits; yet breaking RSA-2048 demands a magic-state error rate on the order of one in ten billion (10⁻¹⁰) — about a million times cleaner than today's 99.99% fidelity [1]. A local lab breakthrough and a hacker draining your wallet tomorrow are separated by a gap of orders of magnitude in engineering.

## The AI half is even weaker

If the quantum-hardware half is still off by orders of magnitude, the AI half of the claim is the most fragile link of all. The "broken within one to one and a half years by AI algorithms" narrative cites OpenAI's mathematical breakthrough as its basis — but that body of work demonstrated no actual attack against ECDSA or elliptic-curve cryptography [2].

The pushback from the field was direct. Yehuda Lindell, head of cryptography at Coinbase, stated there is no evidence whatsoever that the mathematical hardness assumptions behind elliptic-curve cryptography are failing. Cryptographer Adam Back went further and simply called it a "FUD burger" [3]. The gap between AI progress on proving theorems and finding an efficient algorithm to invert a public key is enormous. Equating the former with the latter is a conceptual leap.

## The 10³⁰⁰ argument

Among the voices of doubt, Russian physicist Mikhail Dyakonov's calculation is the most widely circulated. He reasoned it out: describing the state of a system of 1,000 logical qubits requires roughly 2¹⁰⁰⁰, or about 10³⁰⁰, continuous parameters. The number is so absurdly large that he pessimistically declared quantum computing will simply never get there [4].

Dyakonov's math is not wrong — but what he calculated is *direct control*. The magic of quantum error correction (QEC) is precisely that we do not need to control those 10³⁰⁰ parameters. Error-correcting codes filter out physical-layer errors, leaving behind only a small number of logical qubits.

## Kalai's correlated-noise objection

Pushing further, mathematician Gil Kalai offered a revised critique: *correlated noise*. Existing error-correction schemes rest on the assumption that noise is independent across qubits. Once the system scales up, unknown correlated physical interference could cause QEC to fail wholesale [5]. In Google's own experiments, a rare correlated-error event occurring roughly once per hour was observed, with its origin still unclear. The road to scalable quantum computing is far from smooth, and the risk of hitting a wall is objectively real.

## Technology is not linear

Step back and look at the rhythm of technological development. People see only the acceleration that AI assistance brings, yet easily miss the equally massive potential for deceleration on the engineering side. Progress is never linear. And "non-linear" contains both acceleration *and* the stagnation that arrives when physical limits are hit. As systems grow, decoherence, crosstalk, and even microscopic physical mechanisms not yet understood can all bring compute to a halt at some node.

So breaking modern cryptography is a long-distance race stacking physics, mathematics, and engineering on top of one another. It will most likely land years — even a decade or more — out, not within the next year or two.

## The right posture

Facing FUD, the correct stance is neither fear nor blind optimism. What we should actually do is push forward the relevant systems' post-quantum upgrades — for example, migrating to post-quantum address formats. At the same time, we should keep a clear-headed wariness toward rhetoric that manufactures market noise through "quantum terrorism" to harvest retail.

The quantum threat is not in the next year or two, so there is no need to panic. Rather than anxiously chasing the noise, it is better to relax, study the relevant knowledge in advance, safeguard your assets well (for instance, avoid reusing addresses whose public keys have already been exposed), closely watch the post-quantum upgrade progress of core developers, and adapt as circumstances evolve.

## References

- **[1]** Google Quantum AI — *Magic state cultivation* on the Willow processor cut errors ~40x to a logical fidelity of 99.99%; the paper also notes RSA-2048 would require a magic-state error rate near 10⁻¹⁰, roughly a million times cleaner than current results. ([blog.google](https://blog.google/innovation-and-ai/models-and-research/quantum-computing/magic-state-cultivation-quantum-computing/))
- **[2]** OpenAI's October 2026 release of machine-generated mathematics (722 manuscripts) was cited by some as evidence of imminent ECDSA risk, but the publication presented no attack on elliptic-curve cryptography or ECDSA. ([gadgetreview.com](https://www.gadgetreview.com/ai-could-break-bitcoin-in-months-cryptographers-are-taking-the-threat-seriously))
- **[3]** Yehuda Lindell (Coinbase head of cryptography) stated there is "no evidence whatsoever" that elliptic-curve hardness assumptions are failing; Adam Back dismissed the warning as a "fud-burger." ([cryptoreportclub.com](https://cryptoreportclub.com/news/coinbase-cryptographer-calls-drakes-bunker-mode-warning-the-very-definition-of-fud))
- **[4]** Mikhail Dyakonov — *Prospects for Quantum Computing: Extremely Doubtful*: a useful machine needs ~10³ qubits, meaning at least 2¹⁰⁰⁰ ≈ 10³⁰⁰ continuous parameters to control, "which is much, much greater than the number of protons in the Universe." ([arxiv.org](https://arxiv.org/abs/1401.3629))
- **[5]** Gil Kalai's correlated-noise conjecture: realistic noise in entangled qubit pairs is not independent, which — if true — violates the assumptions behind surface-code QEC; he argues the correlations grow with system size. ([quantumintel.tech](https://quantumintel.tech/news/gil-kalai-correlated-noise-quantum-error-correction))
