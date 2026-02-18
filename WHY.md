# Why CraftLearn?


## Guaranteed structure, not random output

Every skill enforces a specific teaching structure. When you run `/explain the prisoner's dilemma`, you always get 8–14 progressive stages following a deliberate arc:

- **The problem** — concrete pain points and misconceptions
- **Core idea** — intuition, mental models, and a first naive approach
- **Refinement** — limitations addressed, alternatives compared, practical improvements
- **Production** — real-world applications, trade-offs, where it shows up in practice
- **Verification** — end-to-end walkthrough, exercises, and key takeaways

That arc is enforced, not suggested. Same structure, every time.


---

## Code that actually runs

Notebook skills generate `.ipynb` files you open and run. After generating a notebook, the toolkit executes every code cell to verify it works. If a cell fails, it gets automatically fixed and retried (up to three times).

So when you run `/notebook-py SQL joins`, you get a notebook where:

- Every code cell has been executed successfully
- Graphs and visualizations actually render
- Import statements point to real packages
- Variable references are consistent across cells

The notebooks generate real plots, diagrams, and pictures — not just code that claims to plot something. A notebook on SQL joins shows a Venn diagram of how joins combine rows. A notebook on caching plots hit rates as cache size grows.

For deeper coverage, `/notebook-deep-py hash tables` follows a naive-to-production progression — you build a working hash table, see where it breaks, and improve it step by step. Every cell in that progression runs too.

This applies to every notebook skill — Python, TypeScript, LeetCode walkthroughs, multi-chapter courses. If it generates code, that code has been run.

---

## Teaching method, not just information

Knowing about pedagogy and consistently applying it are different things. Every skill in the toolkit encodes specific teaching principles:

- **Motivation first** — you always learn *why* something exists before *how* it works
- **Intuition before formalism** — analogies and mental models before definitions and proofs
- **Progressive disclosure** — simple cases first, edge cases and complexity revealed gradually
- **Misconceptions and failure cases** — addressed when relevant, not ignored

The `/explain` skill takes this further. `/learn gradient descent from first principles` builds through a deliberate progression — the problem you're trying to solve, naive approaches that don't scale, the real solution, then production concerns like momentum and local minima. Each stage reveals just enough to motivate the next. That arc is guaranteed, not something you hope the model decides to include.

---

## Follow-up that remembers context

After generating any document, the toolkit suggests specific follow-up topics based on what was covered and what naturally comes next.

The `/explore` skill lets you build on existing content:

```
/learn game theory                                   # generates game_theory.md
/explore game_theory.md Nash equilibrium deeper      # generates nash_equilibrium_deep_dive.md
/explore game_theory.md why cooperation emerges why
                                                     # generates cooperation_why.md
```

Each follow-up reads the original document and builds on it. The deeper explanation knows what equilibrium concepts were already covered. The "why" exploration knows what claims were made and interrogates them.

With chat products, you lose context between sessions. Even within a session, long conversations degrade — you re-explain what you already know and get responses that repeat things you've already read. The toolkit's file-based approach means context is durable. It lives in the generated documents, not in a chat window you'll close.

---

## Multiple formats for how you learn

The toolkit gives you the same topic in whatever format works for you:

- **Prose explanations** (`.md`) — for building understanding from first principles
- **Interactive notebooks** (`.ipynb`) — for running code and experimenting
- **Multi-chapter courses** — for comprehensive coverage of broad topics
- **LeetCode walkthroughs** — for interview prep with tested solutions

You don't need to remember which skill produces which format — just describe what you want:

```
/learn the prisoner's dilemma                        # asks: prose or code?
/learn hash tables as a notebook                     # Python notebook with code examples
/learn hash tables deep dive notebook                # deep-dive notebook: naive to production
/learn gradient descent from first principles        # progressive explanation from first principles
/learn error handling as a typescript notebook        # TypeScript notebook
/learn machine learning course                       # multi-chapter course with syllabus
/learn leetcode 322 coin change                      # LeetCode walkthrough notebook
```

The router figures out which skill to use based on what you said.

---

## Courses with real structure

The toolkit's course skills generate real curriculum, not long single responses:

1. **Syllabus first** — generates a chapter outline and waits for your approval before writing anything
2. **You shape the scope** — add chapters, remove ones you don't need, adjust the depth
3. **Connected chapters** — each chapter references earlier material and uses consistent running examples
4. **Real progression** — concepts build on each other with an explicit dependency graph

Chapter 3 on neural networks references the gradient math from Chapter 2. Chapter 5 on overfitting builds on the train/test splits from Chapter 4. That connective tissue makes the difference between a collection of explanations and an actual course.

---

## Portable output, portable tools

Everything the toolkit generates is a file — markdown or Jupyter notebook. Send a notebook to a colleague, export to HTML, print as PDF, or commit to a repo. What you produce is a real artifact you own and control, not a chat transcript.

The skills themselves aren't locked to one editor. They work across Claude Code, Codex, OpenCode, Cursor, and Windsurf. Your learning workflow doesn't break when you switch tools.

---

The toolkit doesn't replace AI chat. It structures it. Instead of asking an open-ended question and hoping for the best, you get a proven teaching method that produces consistent, verified, well-structured learning material — every time.

## Quick reference

| Dimension | CraftLearn | AI Chat |
|---|---|---|
| **Structure** | Enforced teaching arc per skill | Whatever the model produces |
| **Code** | Every cell executed, verified, auto-fixed | Copy-paste and hope |
| **Teaching method** | Motivation-first, intuition-before-formalism, progressive disclosure — encoded | Applied inconsistently |
| **Follow-ups** | `/explore` builds on generated files with full context | Re-explain each session |
| **Formats** | Prose, notebooks, courses, LeetCode | Text only |
| **Courses** | Syllabus approval, chapter dependencies, running examples | No progression design |
| **Portability** | Real files; works across five coding tools | Locked to one product |
