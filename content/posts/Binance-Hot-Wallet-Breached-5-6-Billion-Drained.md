---
title: "Binance Hot Wallet Breached: $5.6 Billion Drained Overnight"
date: "2026-10-30T12:03:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Crypto"
tags:
  - "BTC"
  - "Ethereum"
  - "Exchange Security"
  - "DeFi"
url: "/Crypto/Binance-Hot-Wallet-Breached-5-6-Billion-Drained"
---

Around 4 a.m., Bitcoin was still hovering near $80k. By mid-morning, it had broken below $77k, down more than 5% over 24 hours. What brought the market down was not macro data, but a string of on-chain transfers.

At 20:24 UTC on October 29, a transaction was sent from an ETH hot wallet flagged as belonging to Binance, moving out 167,464 ETH plus 63 types of tokens, including 1.615 billion USDT, all sent to a freshly generated address[1]. On-chain statistics later put the total at no less than $5.57 billion across three chains. Chainalysis estimated even higher — at $5.912 billion based on prices at the time of the theft, equivalent to four times the 2025 Bybit hack[2].

What truly sends a chill down the spine is the authorization that occurred three minutes and twenty-four seconds before that transaction.

An address funded by the mixer Tornado Cash submitted an EIP-7702 delegation to this hot wallet. EIP-7702 is a change introduced in Ethereum's 2025 Pectra upgrade; it allows an ordinary wallet address — an EOA — to delegate a piece of smart contract code, after which that address behaves more like a contract account. The change was originally meant to solve very practical problems, such as batch transactions, gas sponsorship, and social recovery, letting ordinary wallets use smart-account capabilities[1].

The problem lies precisely in the fact that this delegation is persistent. Odysseas Lamtzidi, founder of Phylax Systems, put it bluntly: EIP-7702 lets an ordinary wallet execute delegated code, and that delegation stays put — the code can later continue to authorize transfers even when the wallet is no longer signing. He had an even sharper line: EIP-7702 can turn the wallet itself into a scavenger[1].

That line is no exaggeration in this incident. The attacker did not need to obtain the private key, nor did they need to move 63 types of tokens out one by one. They only needed to get this hot wallet to accept a delegation, install a piece of self-written code, and the wallet would finish the rest of the work. Three minutes and twenty-four seconds later, the transaction that moved 167,464 ETH was signed by the wallet itself.

What is most puzzling here is not what that code specifically did, but that this delegation had no expiration date at all.

Those familiar with DeFi will not find this unfamiliar. The ERC-20 token approval, also known as approve, is likewise a one-time signature with long-term validity. You click confirm once on a DEX, the approved amount may be set to infinity, and afterward that contract can move your coins at any time without requiring you to sign again. Over the years the industry has paid dearly for this — wallets are littered with stale approvals, and every so often someone gets swept clean, which is why various revoke tools emerged and the habit of setting smaller limits took hold.

EIP-7702 moves the same pitfall onto the wallet itself. A token approval delegates authority to a token contract and can only touch that one coin; but an EIP-7702 delegation delegates a piece of code, and when that code executes, its identity is the wallet itself — it can call any contract and move any asset in that address, including ETH itself. What is worse, a token approval still has a visible limit you can check — open the wallet and you can see who was approved and for how much; an EIP-7702 delegation is hidden in the account's code field, which ordinary users would never look at, and few wallets surface it as a prominent warning.

The designers probably thought that, since the EOA's private key already represents everything, a delegation is merely expressing the same power in code, so no expiration was needed. But in reality, signing scenarios vary wildly. A batch operation to save gas and an authorization that hands over your entire fortune look almost identical on the interface. In the smart-account paradigm, session keys can be given time limits and scopes; EIP-7702 turned an ordinary wallet into a contract account but failed to bring that layer of restriction along.

One transaction, one signature, one authorization with no expiration. Stacked together, these are the true technical backdrop of this incident.

So how was that delegation's signature obtained? This is the deadliest question in the whole affair. Ido Ben-Natan, co-founder of security firm Blockaid, gave a preliminary assessment pointing toward key misuse: the attacker tricked or compromised the signing system into signing malicious transactions, without the underlying private key being extracted. In his words, it looks like the signing infrastructure was compromised, and he does not believe the key was leaked[2]. Binance's own account pointed to a hacker breaking into an engineer's work computer[2].

An eager hacker and an exchange's billions of dollars of assets were separated by nothing more than an ordinary engineer's computer. This is the most stark illustration of the weakest-link effect. The security designs exchanges have stacked up over the years — hot/cold separation, multi-signature, threshold signatures, address whitelists, limit checks — are layered thick, yet as long as any single link in the signing process falls on an ordinary office computer, all the preceding designs become decoration. The attacker does not need to breach the whole castle; they only need to find the unlocked side door.

It would be a mistake to read this as merely some employee's negligence. One person getting phished is the norm and happens in any organization. The real problem is why one person's mistake can be directly converted into billions of dollars of signing authorization. There should have been several gates in between — independent verification, independent approval, independent limit restrictions — but this time, the gates did not hold. That a single point of breach succeeded indicates a systemic flaw in the system itself, not just bad luck.

This incident inevitably recalls 2019. On May 7 of that year, Binance was hacked for over 7,000 BTC, more than $40 million at the time. The industry argued fiercely over it, even briefly attempting to publicly propose rolling back BTC to void the stolen transaction. That episode was later reviewed: the rollback ultimately did not happen, Binance swallowed the loss itself, and Bitcoin's value proposition was preserved.

More than seven years on, the scale of theft has grown from $40 million to $5.9 billion — over a hundredfold. The market has grown ever larger, yet the technology seems not to have kept the same pace. The hurdle back then was overcome by the Bitcoin network's irreversibility and inability to be frozen, preventing a local loss from spreading into an industry-wide bitter pill. This time, what could not hold was the exchange's own signing system — and it was using the newest feature on Ethereum.

The hole now can still be patched with money. Binance said it will use its security fund to cover all losses, and the various stablecoin issuers cooperated to freeze overnight — $3 billion has already been frozen on-chain, and Arbitrum's security council also froze a sum[2]. There is a worry worth stating: exchanges have been highly profitable in recent years and have built up ample security funds, so they can afford to pay. But this account will eventually need a different algorithm. When the industry matures and margins fall, security costs and loss amounts will only rise — will they still be able to afford it then?

Binance's later official line was that the total impact was about $6.3 billion, of which about $3 billion had already been frozen on-chain[3]. In the short term, people care about whether the $3-plus billion outside the freeze can be recovered. But in the long run, we should care more about whether the next time an exchange runs into trouble, it will step into the same river again.

## References

- **[1]** On-chain transaction records of the affected Binance ETH hot wallet; Ethereum Improvement Proposal EIP-7702 (introduced in the Pectra upgrade, 2025); commentary from Phylax Systems founder Odysseas Lamtzidi.
- **[2]** Chainalysis loss estimate; preliminary assessment by Blockaid co-founder Ido Ben-Natan; Binance's statement attributing the breach to a compromised engineer workstation; on-chain stablecoin freezes and the Arbitrum Security Council freeze.
- **[3]** Binance's official figure: total impact approximately $6.3 billion, of which about $3 billion frozen on-chain.
