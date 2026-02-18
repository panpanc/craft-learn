# Coherentism — Deep Dive

> *Going deeper on coherentism from [epistemology_staged.md](epistemology_staged.md), Stages 5 and 13.*

---

## Context Recap

The source introduces coherentism in Stage 5 as one of four responses to the epistemic regress problem. You already know:

- **The regress problem**: every justification rests on a further justification, generating an infinite chain.
- **Coherentism's answer**: reject the chain metaphor entirely. No belief is foundational. Instead, beliefs justify each other through mutual support — a web rather than a pyramid.
- **The raft metaphor**: knowledge is a raft at sea. No single plank is the foundation, but the planks hold together by supporting one another. You can repair any plank, but you can't lift the whole raft out of the water at once.
- **The main objection mentioned**: a perfectly coherent fairy tale is still false. Coherence alone doesn't guarantee truth.

That's roughly one page of a 13-stage document. There's a lot the source leaves unexamined.

---

## Why Go Deeper

The source raises coherentism and moves on quickly, but several critical questions are left hanging:

1. **What does "coherence" actually mean?** The source says beliefs are justified by "fitting well" with everything else you believe. But "fitting well" is vague. Is it just logical consistency? Something more?
2. **How does the justification actually flow?** In foundationalism, justification flows upward from basic beliefs. In coherentism, it flows... where? In circles? Everywhere at once? How does that work without being viciously circular?
3. **How do you choose between two equally coherent but incompatible systems?** The fairy tale objection is mentioned but not resolved. Do coherentists have an answer?
4. **What's the relationship between coherence and truth?** If coherence doesn't guarantee truth, why should we care about it?
5. **Can coherentism handle the introduction of new beliefs?** When you learn something genuinely new, how does it enter the web?

Let's take these layer by layer.

---

## Layer 1 — Mechanics: What "Coherence" Actually Means

The source uses "coherence" as though it's a single, intuitive concept. It isn't. Epistemologists have identified at least five distinct ingredients, and the theory's plausibility depends on which ones you include.

### Ingredient 1: Logical Consistency

The minimum requirement. A coherent belief system contains no outright contradictions.

**Example — an incoherent system:**

| Belief | |
|---|---|
| $B_1$: All mammals are warm-blooded | |
| $B_2$: Whales are mammals | |
| $B_3$: Whales are cold-blooded | |

$B_1$ and $B_2$ together entail "whales are warm-blooded," which contradicts $B_3$. The system is logically inconsistent, so it fails the most basic coherence test.

But consistency alone is far too weak. The set $\{$"Snow is white," "Caesar crossed the Rubicon," "Quarks have color charge"$\}$ is perfectly consistent — the beliefs don't contradict each other — but they're also completely unrelated. Nobody would call that a coherent system. So we need more.

### Ingredient 2: Explanatory Relations

Beliefs should *explain* each other. A coherent system isn't just a pile of non-contradictory claims — it's an interconnected network where beliefs provide reasons for other beliefs.

**Example — adding explanatory structure:**

| Belief | Explains / Is explained by |
|---|---|
| $B_1$: The streets are wet | Explained by $B_2$ |
| $B_2$: It rained last night | Explains $B_1$; explained by $B_3$ |
| $B_3$: The forecast predicted rain | Supports $B_2$ |
| $B_4$: Dark clouds were visible yesterday evening | Supports $B_2$ and $B_3$ |

Now the beliefs form a network where each one is connected to others by explanatory or evidential links. This is closer to what coherentists mean.

### Ingredient 3: Inferential Density

The *more* connections between beliefs, the more coherent the system. A belief that connects to many others is better supported than one connected to few.

Think of it like a graph:

```
  Sparse (low coherence):          Dense (high coherence):

    A       B       C              A ←──→ B ←──→ C
                                   ↑  ╲   ↑   ╱  ↑
                                   │    ╲  │  ╱   │
                                   D ←──→ E ←──→ F
```

In the dense graph, removing or revising any single node still leaves the others well-supported. In the sparse graph, each belief stands alone.

### Ingredient 4: Absence of Unexplained Anomalies

A coherent system shouldn't contain beliefs that *should* be explained by other beliefs but aren't. If your system includes "the streets are wet" but has no explanation for *why* they're wet, that's an anomaly that reduces coherence.

### Ingredient 5: Predictive Unity

The beliefs in a coherent system should, taken together, generate predictions that are themselves confirmed. This is where coherentism starts to resemble the structure of scientific theories — a network of claims that mutually support each other and collectively predict observable outcomes.

### Putting It Together

Coherence, properly understood, is a *multidimensional* property:

$$\text{Coherence}(S) = f(\text{consistency}, \text{explanatory connections}, \text{inferential density}, \text{anomaly absence}, \text{predictive unity})$$

No single ingredient is sufficient. The theory's strength comes from requiring *all* of them simultaneously.

---

## Layer 2 — Under the Hood: How Justification Flows Without a Foundation

### The Circularity Objection — and Why It Misses the Point

The most common objection to coherentism is: "It's circular. A justifies B, B justifies C, C justifies A. That's a logical fallacy."

This objection treats coherentist justification as if it were a *linear argument*. But coherentists reject the linear model entirely. The justification isn't a chain; it's a *holistic* property of the entire system.

Here's the crucial distinction:

**Linear circularity (fallacious):**

```
  "Why believe A?"  →  "Because B"
  "Why believe B?"  →  "Because C"
  "Why believe C?"  →  "Because A"
```

This is indeed viciously circular. Each step pretends to offer independent support, but the support runs in a closed loop.

**Holistic coherence (what coherentists actually claim):**

No individual belief is justified by tracing a path through other beliefs back to itself. Instead, the *entire system* has the property of coherence, and each belief is justified by being a member of a maximally coherent system.

An analogy: consider a jigsaw puzzle. No single piece "supports" another in a linear chain. But when all the pieces interlock, each piece is confirmed as correct *by the pattern formed by all the others together*. You don't validate piece 47 by tracing a chain from piece 1 through piece 2 through... piece 46. You validate piece 47 because it fits the overall picture.

### The Formal Structure: BonJour's Conditions

Laurence BonJour, the most prominent 20th-century coherentist, proposed specific conditions a belief system must meet. Simplified:

1. The system must be **logically consistent**.
2. The system must be **inferentially connected** — beliefs must bear logical, explanatory, or probabilistic relations to each other.
3. No subsystem should be **inferentially isolated** from the rest. (No "floating islands" of beliefs unconnected to the mainland.)
4. The system should be **relatively stable under new input** — incorporating a new belief shouldn't require overhauling everything.
5. **Anomalies** (unexplained conflicts with observation or with other beliefs) should be few and diminishing over time.

### Degrees of Justification

In foundationalism, justification starts at maximum strength (basic beliefs are self-evident) and *degrades* as it travels upward through inference. In coherentism, justification is a property of the *system's global structure*, and individual beliefs partake of it to varying degrees:

$$J(B_i) \propto \text{(number and strength of connections between } B_i \text{ and the rest of } S\text{)}$$

A belief deeply embedded in the web — connected to many others by strong explanatory and evidential links — is more justified than a peripheral belief connected by a single thread. This gives coherentism a natural account of *degrees* of justification, something foundationalism struggles with.

```
  Highly justified (central):        Weakly justified (peripheral):

        ╱─ B₂                              B₇
       ╱                                     │
  B₁ ─── B₃                                 B₈
       ╲
        ╲─ B₄ ─── B₅
```

$B_1$ participates in many relations; $B_7$ hangs by a single connection.

---

## Layer 3 — Edge Cases and Failure Modes

### Failure Mode 1: The Fairy Tale Problem (The Isolation Objection)

The source mentions this: a perfectly coherent fairy tale is still false. Let's make the objection precise.

**Scenario**: Consider two belief systems.

*System A* (roughly corresponds to reality):
- Physical objects exist independently of observers
- Perception is generally reliable
- Scientific theories are approximately true
- ...connected by millions of explanatory links...

*System B* (a coherent fiction):
- The world was created last Thursday with all memories and evidence pre-installed
- Physics works as observed, but only because the creator designed it that way
- Every piece of "evidence" for a longer history was fabricated
- ...also internally consistent, also explanatorily connected...

Both systems are equally coherent by the criteria above. System B explains every observation just as well as System A (by design — it was constructed to). How do you choose?

**The coherentist response** (BonJour): the coherentist doesn't claim coherence *alone* determines truth. The theory requires an additional element — **observation**. Your belief system must cohere not just internally, but with your ongoing perceptual experience. You have spontaneous, involuntary perceptual beliefs ("I see a red thing in front of me") that serve as *input* to the coherence evaluation.

This is where coherentism gets subtle. These perceptual beliefs aren't *foundational* — they can be overridden by the rest of the system (optical illusions, known unreliable conditions). But they do provide an external constraint that prevents the theory from floating free of reality.

Critics respond: this looks suspiciously like smuggling in foundationalism. If perceptual beliefs play a special, constraining role, aren't they *functionally* basic beliefs? BonJour spent decades wrestling with this tension, and eventually conceded significant ground (more on this in the summary).

### Failure Mode 2: The Alternative Systems Problem

Even with the observational constraint, there may be multiple incompatible systems that are equally coherent with your experience. Consider:

| System | Core commitment | Coherent with all observations? |
|---|---|---|
| Scientific realism | Unobservable entities (atoms, fields) really exist | Yes |
| Instrumentalism | "Atoms" are useful fictions; only observations are real | Yes |
| Idealism | Only minds and ideas exist; "physical objects" are patterns in experience | Yes |

All three systems can accommodate every possible observation. If coherence is the sole criterion for justification, all three are equally justified. But they make fundamentally different claims about reality.

**The coherentist response**: invoke further coherence criteria. Scientific realism may be more coherent in the *explanatory unity* dimension — it explains *why* the "useful fictions" work, while instrumentalism treats their success as a brute fact. This is a genuine argument, but whether it's decisive is debatable.

### Failure Mode 3: The Diachronic Problem (Belief Change Over Time)

How does a coherentist handle *learning*? When you encounter genuinely new information that conflicts with your existing web, what happens?

**Scenario**: You believe the source document's claim that the regress problem has four options (infinite regress, circularity, foundation, skepticism). Then you read a paper arguing there's a fifth option — *contextualism* (justification standards shift depending on context).

Your current web has no place for this belief. It doesn't cohere with the "exhaustive four options" framing. Do you:

(a) Reject the new belief to preserve coherence?
(b) Accept it and revise the "four options" belief?
(c) Something else?

Coherentism says: choose whichever revision produces the *most coherent* overall system. This is analogous to the Quinean idea of a "web of belief" where we revise at the periphery (empirical beliefs) before the core (logic, mathematics), minimizing total disruption.

But "maximally coherent revision" is computationally intractable — you'd need to evaluate the coherence of every possible way to adjust your beliefs and pick the best one. In practice, humans use heuristics (trust recent perception over old memory, trust experts over laypeople, prefer simpler explanations). Whether these heuristics can be *derived from* coherentism or must be added as external constraints is an open question.

### Failure Mode 4: The Preface Paradox

Consider an author who writes a 200-page book. She believes every individual claim in the book. But she also writes in the preface: "This book surely contains errors." This is perfectly rational — she'd be arrogant to think she got everything right. But now her belief system is:

- $B_1$: Claim 1 is true
- $B_2$: Claim 2 is true
- ...
- $B_{200}$: Claim 200 is true
- $B_P$: At least one of $B_1$ through $B_{200}$ is false

This system is *logically inconsistent*. Yet every individual belief in it seems justified. Coherentism, which requires logical consistency as ingredient #1, seems to demand she give up either $B_P$ (become arrogant) or some arbitrary $B_i$ (abandon a belief she has no specific reason to doubt).

This isn't a knock-down objection — foundationalism faces it too — but it highlights that coherentism's consistency requirement creates pressure in cases involving large, complex belief systems where some error is statistically inevitable.

---

## Connections Back

With this deeper understanding of coherentism, re-read the source document and notice several things:

1. **The raft metaphor is deeper than it looks.** When the source says "you can repair any plank but can't lift the whole raft out of the water at once," that's actually encoding a precise epistemological thesis: you can *revise* any individual belief, but you can't step outside your entire belief system to evaluate it from a neutral vantage point. There is no Archimedean point. This is one of coherentism's most radical claims.

2. **The source's own structure is coherentist.** Look at how the 13 stages work: each stage introduces a concept that connects to multiple other stages. The Gettier problem (Stage 3) motivates reliabilism (Stage 9). The regress problem (Stage 5) connects to skepticism (Stage 6) and responses to skepticism (Stage 7). The source document is itself a web of mutually supporting ideas, not a foundation-up tower. The source demonstrates coherentist structure while teaching about it.

3. **The fairy tale objection deserves a footnote.** The source presents it as a straightforward refutation, but as we've seen, mature coherentism has a response: observational constraint. The objection lands against a straw-man version of coherentism that ignores perceptual input. Whether the response *succeeds* is another question, but the source could have presented the dialectic more fairly.

4. **The foundationalism vs. coherentism framing is too clean.** The source presents them as distinct alternatives. But BonJour's concessions and the development of "modest foundationalism" have blurred the boundary. Most contemporary epistemologists hold views that borrow from both — e.g., foundherentism (Susan Haack), which combines foundational perceptual inputs with coherentist holistic justification. The real landscape is a spectrum, not a binary.

---

## Summary and References

### Key Insights

- **Coherence is multidimensional**: logical consistency, explanatory connections, inferential density, anomaly absence, and predictive unity. Not just "beliefs that don't contradict each other."
- **The circularity objection misunderstands the theory**: coherentism claims holistic, non-linear justification, not circular chains of inference.
- **Observational constraint is essential**: without it, coherentism can't distinguish reality from fiction. With it, coherentism starts to look like foundationalism in disguise — a tension the theory has never fully resolved.
- **Coherentism handles degrees of justification naturally**: beliefs embedded in more connections are more justified, without needing to posit a special class of "basic" beliefs.
- **The theory faces real problems**: alternative systems, diachronic belief change, and the preface paradox all push on genuine weaknesses.
- **The foundationalism/coherentism divide is less sharp than textbooks suggest**: the most defensible positions borrow from both traditions.

### References

1. **BonJour, L. (1985).** *The Structure of Empirical Knowledge.* Harvard University Press. — The definitive 20th-century defense of coherentism. Chapters 5–8 lay out the formal conditions discussed in Layer 2.
2. **Haack, S. (1993).** *Evidence and Inquiry: Towards Reconstruction in Epistemology.* Blackwell. — Introduces "foundherentism," a hybrid of foundationalism and coherentism. The crossword puzzle analogy in Chapter 4 is especially illuminating.
3. **BonJour, L. (1999).** "The Dialectic of Foundationalism and Coherentism," in *The Blackwell Guide to Epistemology*, ed. Greco and Sosa. — BonJour's partial recantation, conceding that coherentism needs something like foundational perceptual input.
4. **Olsson, E. (2005).** *Against Coherence: Truth, Probability, and Justification.* Oxford University Press. — The strongest formal case against coherentism, using probabilistic models to argue that coherence doesn't reliably track truth.
5. **Quine, W.V.O. (1951).** "Two Dogmas of Empiricism," *The Philosophical Review* 60(1). — The "web of belief" metaphor that undergirds much coherentist thinking, even though Quine himself didn't identify as a coherentist.
