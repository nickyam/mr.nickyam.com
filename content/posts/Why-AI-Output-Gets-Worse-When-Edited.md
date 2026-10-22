---
title: "Why AI Output Gets Worse the More You Edit It (and How to Fix It)"
date: "2026-10-21T08:17:00+08:00"
author: "Nick Yam"
toc: true
categories:
  - "Tech"
tags:
  - "AI"
  - "DeepSeek"
  - "LLM"
  - "Prompting"
url: "/Tech/Why-AI-Output-Gets-Worse-When-Edited"
---

A common observation: AI-generated content looks decent on the first pass, but ask the model to revise it and the result often turns into a mess. Why?

Two AI assistants were asked to explain. Their answers are reproduced below.

## DeepSeek's explanation [1]

The phenomenon is widespread enough that the industry even has a phrase for it: "the more you edit AI copy, the worse it gets." The cause is not a single factor but a stack of several mechanisms:

1. **Context pollution (the core issue).** Every time the model revises, it stuffs the original draft, your edit request, and its own previous output back into the context and regenerates. The wording, structure, and even errors you disliked in the previous round all become "reference material" for this round. The more rounds, the more "garbage" piles up in the context, and the easier it is to be led astray. It is like asking someone to keep tracing over handwriting that is already crooked — the more they trace, the blacker and messier it gets.

2. **Instruction stacking causes goal drift.** You say "make it more concise," so it deletes; then "but don't lose the details," so it adds back; then "make the tone livelier," which breaks the balance of the first two. Multi-round instructions often carry hidden conflicts. The model has no real "global plan" and optimizes locally each round, so the whole thing becomes increasingly awkward.

3. **It tends to over-respond.** The model is trained to be highly sensitive to user instructions. Point out a flaw and it amplifies the change in that direction, sometimes altering parts that were fine. You ask it to fix A, and it quietly moves B and C too — drifting further from the draft in your head.

4. **No "version memory."** Human editing works from a fixed baseline. The model regenerates each round and does not truly "remember" what was good about version one; it only samples probabilistically from the current context. That "formed-in-one-pass" coherence of the first version is hard to reproduce in later rounds.

5. **Accumulation of sampling randomness.** Every generation carries randomness; across multiple rounds, stylistic consistency drifts. The first version may have happened to sample a harmonious combination, but later rounds often do not.

Practical countermeasures:

- Don't keep editing a bad draft. Return to the good first version and issue a fresh edit request, rather than iterating on the broken result.
- Request only one dimension of change at a time; confirm before raising the next, to avoid conflicting instructions.
- Spell out what *not* to touch — e.g., "only revise the second paragraph; keep everything else as is."
- Process important content in segments; don't funnel the whole piece into one context.
- If it is truly stuck, have the model rewrite from the original rather than "edit on top of the last version."

In short: AI editing is not "editing" so much as "improvising anew each time," so the more you iterate, the further you stray from the baseline you were happy with.

## Doubao's explanation [2]

The core point first: it is not that the AI's "memory gets worse," but that a second revision is a constraint-stacking problem — the more you edit, the messier the goal and the more the weights drift. Broken down plainly:

1. **First generation: clean goal, high freedom.** Your first prompt is a single, clear instruction — say, "draft a song list for a park choir" or "write a group announcement." The model converges toward that one goal in its vast knowledge space and produces a balanced, coherent result. With no old-text baggage, it only needs to satisfy your immediate request, so it easily produces something that looks reasonable.

2. **Second revision: it must juggle three conflicting things at once.** When you say "revise this part," the model receives three implicit tasks: (1) keep most of the original; (2) satisfy your new request; (3) preserve style, length, and logic. These three routinely conflict. You only asked to change point A, but the model over-imagines and also moves B, C, and D — large models lack the native ability to "precisely change one sentence and leave everything else untouched"; they rewrite holistically, not like Word's pinpoint editing. Your new request may also implicitly contradict your original need; the first pass followed logic A, the second adds B, and since it does not know which has priority, it compromises — and the compromise looks neither here nor there.

A familiar example: you ask for a saxophone song list (good first pass), then say "make it leaner, suited to a 60-year-old male voice." It does not know which items are your must-keeps, so it easily deletes key pieces and randomly adds unsuitable ones.

3. **The "weight dilution" of the context window.** The longer the conversation, the lower the weight of the earliest original request in the model's eyes. The model does not pin "the first sentence's requirement" to the top like a human does. As information piles up in the context, the latest instruction gets the highest weight while the earliest need slowly fades. By the third or fourth edit, it may even forget the original core purpose and fixate only on your latest fragmentary request, so the output naturally goes off the rails.

4. **The model's probabilistic nature (the root cause).** A large model does not "retrieve a standard answer"; it predicts the next token probabilistically.

- First sampling: luck plus prompt match lands on the branch you liked.
- The very same prompt produces a different result the second time.
- Modifying on top of old text is like forcing a turn onto an already-determined probability path — it easily slides into an incoherent branch, and sentences, logic, and style collapse. Even if you demand "don't change anything else," it struggles to comply strictly; this is an inherent shortcoming of autoregressive generation.

A practical fix (use this going forward):

Avoid the pattern [generate → immediately say "change it"]. Switch to one of two approaches:

1. Copy the satisfying first draft + write clear, pinpoint edit instructions. Template:

> Original: [paste the full satisfying version]
> Edit request: modify only this one spot, XX; leave all other text, structure, and style completely unchanged; do not add or remove anything else.

2. If it breaks, return to the originally satisfying version and start over. Don't keep stacking edits on top of an already-broken version — the more you stack, the messier it gets.

One more note: some AIs offer an "edit mode / pinpoint modification," which works by adding extra controls that constrain the change scope. Ordinary chat mode is inherently unsuited to repeated fine-tuning.

## References

- **[1]** The five-point explanation — context pollution, instruction-stacking goal drift, over-response, lack of version memory, and accumulated sampling randomness — together with the practical countermeasures, is drawn from a DeepSeek response as cited in the source article.
- **[2]** The constraint-stacking analysis and the "copy good draft + pinpoint edit instruction" template are drawn from a Doubao response as cited in the source article.
