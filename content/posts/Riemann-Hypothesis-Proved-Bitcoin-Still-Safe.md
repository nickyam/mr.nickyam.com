---
title: "If the Riemann Hypothesis Is Proved, Is Bitcoin Still Safe?"
date: "2026-11-23T12:16:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "Bitcoin"
  - "Security"
  - "Cryptography"
url: "/Crypto/Riemann-Hypothesis-Proved-Bitcoin-Still-Safe"
---

A breakthrough on a century-old problem has arrived in mathematics.

On November 20, 2026, mathematician Levent Alpöge announced that, with the help of the AI system Claude, he had completed a proof of the Riemann Hypothesis and released roughly 17 million lines of Lean code [1].

The stakes are considerable. The Riemann Hypothesis is one of the seven Millennium Prize Problems published by the Clay Mathematics Institute, and a large body of papers and theory is built on the assumption that it is true.

Cautiously, though: as of November 23, 2026, the Clay Mathematics Institute's website still lists the Riemann Hypothesis as unsolved. Formal verification of the proof has made major progress, but a deeper understanding of the argument within the mathematical community, and the formal review for the Millennium Prize, each follow their own procedures [2].

So it is worth letting the dust settle before drawing conclusions.

Yet clickbait outlets have begun running headlines along the lines of "the Riemann Hypothesis is proved, Bitcoin is in danger." Such headlines are easy to ignore, but many readers have been asking whether the news actually matters for Bitcoin.

To keep the discussion grounded: I am neither a mathematician nor a cryptographer, and the working principle here is simple — if something cannot be verified, do not treat it as imminent.

Plenty of those headlines probably never explain what the Riemann Hypothesis is, so that is a reasonable place to start.

## Primes and the question the hypothesis asks

Begin with a simple question.

2, 3, 5, 7, 11, 13 — what do these numbers have in common?

They are all prime numbers.

A prime is a positive integer divisible only by 1 and itself. Take 7: it can be divided only by 1 and 7, and cannot be broken into the product of two smaller integers.

Primes look ordinary, yet they occupy a special place in mathematics.

Think of them as the building blocks of the integers: almost every integer greater than 1 can be decomposed into a product of primes. For example, 12 = 2 x 2 x 3, and 30 = 2 x 3 x 5.

However large a number is, in principle it has a prime factorization. This matters because primes underpin the multiplicative structure of the integers — and that raises a question.

How are primes distributed?

Starting from 2, primes seem dense; as numbers grow, primes become less frequent. Across a long stretch of numbers you may encounter many primes, or none for quite a while.

They look patterned, yet resist any simple pattern. So mathematicians have long tried to find a rule — to work out how primes are distributed as numbers grow, and whether we can estimate in advance roughly how many primes lie below a given enormous number. That is the prime number theorem: in simple terms, it describes the average distribution of primes. It helps estimate how many primes fall within a very large range, but it does not go far enough.

We know the average trend, but not how far the actual distribution deviates from it. An everyday analogy helps.

Suppose a city's average annual rainfall is 900 mm. That tells you the minimum flood-control standard for a reservoir and helps you size it reasonably. But for you personally, deciding whether to carry an umbrella tomorrow, that 900 mm average is useless.

The prime number theorem gives the annual average; the Riemann Hypothesis asks about the range of variation. And as noted above, Riemann himself never claimed to have proved it — he wrote that it was "very probable," then used the assumption as a ladder from which to derive a string of results.

In short, the Riemann Hypothesis imposes a very precise constraint on the distribution of primes, telling mathematicians how large the deviation between the actual distribution and the average can be.

Why does it matter? Because primes run through nearly all of number theory — from integer factorization to number-theoretic functions to modern cryptography. If the hypothesis holds, mathematicians can state with greater accuracy a range of conclusions about prime distribution.

## The first lock: elliptic curves

By now some readers may be losing patience, ready to reach through the screen and ask: does it affect Bitcoin's security or not?!

There is no need to panic. What we have discussed so far is mathematics; Bitcoin is cryptography, and cryptography can be thought of as a set of mathematical rules.

That system has to solve one problem: let others verify that you are entitled to use an asset, without letting them work backwards from public information alone to the secret you hold. That is the value of the system, and the core that supports its future.

The two key concepts are the private key and the public key.

You can think of a private key as a key only you hold, and a public key as public information generated from it through mathematics. A wallet derives the public key from the private key. Others can use your public key to verify transactions you sign, but cannot readily work backwards from it to the private key.

Bitcoin uses elliptic curve cryptography, which rests on a hard problem called the elliptic curve discrete logarithm problem.

The name sounds complicated, but the idea is simple: given a secret number, a defined set of rules lets you easily compute another, public number. Going from the secret to the public number is fast; going the other way — finding the original secret from the public number alone — requires enormous computational cost with known classical methods. That is the basic idea of elliptic curve cryptography.

The curve Bitcoin uses is secp256k1, with a compact equation; all operations take place within the range set by a 256-bit prime. The private key is a large integer, and the public key is obtained by "multiplying" a fixed point by it:

Q = d x G

Put simply, all the computation follows a fixed mathematical rule and the results stay within a defined range [3].

Simple as the formula looks, that multiplication is not ordinary multiplication — it is the fixed point G added to itself d times on the curve. Using a doubling-and-adding technique, a computer can derive the public key from a 256-bit private key in a few hundred operations, fast enough to be negligible. And note that the prime involved is very large, on the order of 256 bits.

So, keeping a cool head, we should ask a rational question: since Bitcoin's mathematical tools involve primes, could the distribution rules studied by the Riemann Hypothesis affect the security of elliptic curves?

Again, there is no need to rush — we still need to understand Bitcoin's second lock. Bitcoin has two locks for encryption; we have covered the first, now the second: SHA-256.

## The second lock: SHA-256

If elliptic curves mainly handle transaction authorization, SHA-256 in Bitcoin's network handles hashing, block chaining, and proof of work — including the mining everyone is familiar with. Miners repeatedly change data in the block header and recompute hashes until they find a result that meets the network's difficulty target; that process uses double SHA-256.

Hash functions have an interesting property: change the input slightly and the resulting hash can be completely different. Think of it as a special blender: whether you feed in a sentence, an image, or an entire block, you get a fixed-length result, and working backwards from that result to the original data is computationally infeasible.

Here is an interesting detail. When SHA-256 was designed, numbers related to primes were indeed used as some of its initial constants — taken from the fractional parts of the square roots and cube roots of the first few primes. Superficially, that seems to link it to the Riemann Hypothesis as well. But these are simply fixed numbers chosen at design time. SHA-256 does not need the Riemann Hypothesis to run, and its security does not depend on whether the hypothesis is true [4].

So Bitcoin's security system involves two important tools: elliptic curve cryptography for keys and transaction authorization, and the SHA-256 hash function for data integrity, block chaining, and proof of work. They solve different problems.

## Does the proof change anything?

Which brings us back to the headline: if the Riemann Hypothesis has been proved, is Bitcoin still safe?

The answer is a little surprising. The two are connected mathematically, but far less directly than most people imagine.

The Riemann Hypothesis studies how primes are distributed across the sequence of natural numbers. Bitcoin uses primes. One uses them; the other studies them.

The distinction is something like the difference between clipping your nails and performing surgery — they may sound vaguely related, but that is all.

Here is the line to remember:

Bitcoin's cryptography uses mathematical tools related to primes, but its security does not rest on the assumption that the Riemann Hypothesis is true.

Consider it from a speculative angle: what would happen to Bitcoin if the Riemann Hypothesis were formally proved, or one day disproved?

First, suppose it is eventually proved true. That would give mathematicians a firmer theoretical foundation for prime distribution, advance mathematical research, and potentially refine the analysis of some algorithms that depend on number-theoretic results. But Bitcoin would not automatically become more secure. Your private key would not get longer, your public key would not change, and SHA-256 would not suddenly become safer. Bitcoin's consensus rules, cryptographic parameters, and transaction verification methods would not change because of a mathematical proof.

Now the reverse: suppose mathematicians eventually find the hypothesis false, uncovering a counterexample to the original claim. That would indeed be a major event in the history of mathematics. Many theoretical results that depend on it would need re-examination, and some researchers' directions might shift. But it still would not directly imply that Bitcoin's cryptographic system has been broken, because disproving the Riemann Hypothesis and finding an algorithm that quickly solves the elliptic curve discrete logarithm problem are two different things. Only if follow-up research actually produced a usable new algorithm — one capable of effectively attacking existing cryptographic systems under real-world computing conditions — would a genuine security threat arise.

As of now, the work on proving the Riemann Hypothesis has produced no such result. So whether it is proved true or eventually disproved, that fact alone is not enough to conclude that Bitcoin's security has changed.

## Closing thoughts

This has run a bit long, so a few closing reminders. Whether you have been in this space since 2017 or arrived only recently, one point matters: cryptographic security and asset-management security are two separate questions.

The Riemann Hypothesis remains an extraordinary mathematical problem. It studies the patterns behind prime numbers and helps us understand the world of numbers more deeply.

Bitcoin, meanwhile, is a system that combines mathematics, cryptography, computer networks, and economic incentives. The two overlap mathematically, yet each has its own independent questions.

We should absolutely pay attention to advances in mathematics and technology, especially breakthroughs that might shift the boundaries of cryptographic security. But there is no need to see progress on a famous math problem and start worrying whether your wallet will open tomorrow. Understanding the boundaries of a technology matters far more than panicking at a new term.

Verify, don't trust.

That maxim applies to investing, and it applies just as well to technology.

1 BTC = 1 BTC.

At least today, progress on the Riemann Hypothesis has not changed that.

A sense of security should come from understanding the assumptions, not from associations with a name.

Wishing you a steady mind through the cycles.

## References

- **[1]** Levent Alpöge's November 20, 2026 announcement of a formalized proof of the Riemann Hypothesis with assistance from the AI system Claude, published as roughly 17 million lines of Lean code.
- **[2]** Clay Mathematics Institute — the Riemann Hypothesis remains listed among the seven unsolved Millennium Prize Problems as of November 23, 2026.
- **[3]** Bitcoin's use of the secp256k1 elliptic curve and the relation Q = d x G for deriving a public key from a private key.
- **[4]** The SHA-256 algorithm: its use of double hashing in Bitcoin mining and its initial constants derived from the square roots and cube roots of the first few primes.
