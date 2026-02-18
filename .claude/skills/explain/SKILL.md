---
name: explain
description: Generate a markdown document that explains a concept through progressive stages
---
Generate a markdown document that explains a concept through progressive stages.

## Perspective

Explain as an engineer and educator who:
- Starts from the problem, not the solution
- Values "working code you can trace by hand" over abstract descriptions
- Builds intuition through concrete examples before generalizing
- Treats each stage as answering a natural "but what about...?" question

## Instructions

1. **Parse arguments**: The user provides a topic as: $ARGUMENTS. For example: `"universal hashing"`, `"B-trees"`, `"gradient descent"`.

2. **Design the stages**: Break the topic into 8–14 progressive stages. Each stage should:
   - Start with a **"Motivation"** section explaining *why* this step is needed (what problem it solves, what gap it fills)
   - Include **"Intuition"** — use analogies, mental models, or "think of it like..." explanations to make abstract ideas click
   - Follow with clear explanations, diagrams (ASCII where helpful), and examples
   - Use concrete, small examples so the reader can trace through by hand
   - Build on previous stages — later stages should reference or extend earlier concepts

3. **Stage structure** (follow this arc):
   - **Stages 0–1:** The problem / what we're trying to achieve (concrete examples of the pain point, common misconceptions about the problem)
   - **Stages 2–4:** Core idea and first naive approach (show the math/intuition, explain how it works, show what goes wrong with a broken or naive attempt). Address common misconceptions — name the wrong mental model and explain why it's wrong
   - **Stages 5–7:** Refine the approach (address limitations, compare with alternatives, add practical improvements). Address common misconceptions — name the wrong mental model and explain why it's wrong
   - **Stages 8–10:** Production considerations (optimizations, trade-offs, real-world usage, where this shows up in practice)
   - **Final stages:** End-to-end walkthrough, verification (prove a key claim with a worked check or empirical test), common pitfalls to watch for, when this approach does *not* apply or breaks down, generalizable pattern (what transfers beyond this specific topic), key takeaways summary, and 2-3 practice exercises the reader can try

4. **Writing style**:
   - Use clear, conversational prose — explain like teaching a colleague
   - Prioritize *why* over *what* — always explain the reasoning behind each concept
   - Build intuition before formalism — use analogies and mental models first, then introduce precise definitions
   - Include concrete examples with specific numbers/data the reader can verify
   - Add ASCII diagrams or tables where they aid understanding
   - Highlight key insights and "aha moments" explicitly
   - Include code snippets (in fenced code blocks) where they clarify implementation details
   - Include at least one "what goes wrong without this" example — show the failure that motivates the concept
   - End each stage with a brief transition to the next

5. **Naming**: Save the document in the current working directory as `<topic_slug>.md` (e.g., `universal_hashing.md`).

6. **Progress**: After completing the file, print a brief summary of what was generated:
   `Generated <N> stages covering: <stage 0 title> → ... → <final stage title>`

7. **Follow-up suggestions**: After saving, print a brief "What's next?" block with 2-3 contextual follow-up commands using the actual generated filename. For example:

   > **What's next?**
   > - Drill into a stage: `/explore <filename> <stage topic> deeper`
   > - Interrogate a claim: `/explore <filename> <claim> why`

   Use the actual generated filename and pick a stage topic from the document.

## Example usage

```
/explain universal hashing
/explain B-trees
/explain gradient descent from scratch
/explain how TCP congestion control works
/explain the raft consensus algorithm
```
