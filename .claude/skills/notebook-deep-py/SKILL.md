---
name: notebook-deep-py
description: Create a deep-dive Python notebook that explains a concept from first principles with illustrative code examples
---
Create a deep-dive Python notebook that explains a concept from first principles with illustrative code examples.

## Perspective

Explain as an engineer and educator who:
- Writes code that teaches, not just code that works
- Shows the evolution from naive to production-quality
- Makes every line of code earn its place with visible output
- Values "I could have written this myself" clarity
- Treats each stage as answering a natural "but what about...?" question

## Instructions

1. **Parse arguments**: The user provides a topic as: $ARGUMENTS. For example: `"universal hashing"`, `"B-trees"`, `"gradient descent"`.

2. **Design the stages**: Break the topic into 8–14 progressive stages. Each stage should:
   - Start with a **"Motivation"** section explaining *why* this step is needed (what problem it solves, what gap it fills)
   - Include **"Intuition"** — use analogies, mental models, or "think of it like..." explanations to make abstract ideas click before showing code
   - Follow with **working Python code** that demonstrates the concept concretely
   - Use small, inspectable data so the reader can trace through results by hand
   - Build on previous stages — later code should reference or extend earlier code

3. **Stage structure** (follow this arc):
   - **Stages 0–1:** The problem / what we're trying to achieve (concrete examples of the pain point, common misconceptions)
   - **Stages 2–4:** Core idea and first naive implementation (make it work, show the math/intuition, include a cell showing what goes wrong with a broken or naive attempt). Address common misconceptions — name the wrong mental model and explain why it's wrong
   - **Stages 5–7:** Refine the implementation (address limitations, compare approaches, add practical improvements). Address common misconceptions — name the wrong mental model and explain why it's wrong
   - **Stages 8–10:** Production-quality version (clean class/module, optimizations, benchmarks)
   - **Final stages:** End-to-end demo, real-world applications, verification (prove a key claim with a worked check or empirical test), common pitfalls to watch for, when this approach does *not* apply or breaks down, generalizable pattern (what transfers beyond this specific topic), key takeaways summary, and 2-3 practice exercises the reader can try

4. **Diagrams and visualizations**: Use matplotlib to make abstract ideas
   concrete. Aim for 3-5 visuals across the stages — not decoration, but
   explanatory tools. Distribute them where they have the most impact:
   - **Early stages (0–2):** A diagram of the problem space or data structure
     layout to ground the reader before any code
   - **Middle stages (3–6):** Step-by-step algorithm traces, before/after
     comparisons, or "what went wrong" failure visualizations
   - **Late stages (7+):** Performance curves (empirical O(n) vs O(log n)),
     benchmark bar charts, or architecture diagrams of the final design

   When a concept is spatial or structural, a diagram is mandatory — don't
   rely on prose alone. Use simple, labeled plots with clear titles. Prefer
   `plt.figure(figsize=(...))` over defaults for readability.

5. **Code style**:
   - Every code cell should produce visible output (prints, plots, or assertions)
   - Include at least one benchmark or empirical verification
   - Prefer self-contained code — each cell should run independently after running prior cells
   - Use only standard library + common packages (numpy, matplotlib, etc.)
   - Highlight key insights and "aha moments" explicitly — use markdown cells to call out the crucial realization
   - End each stage with a brief transition to the next — what question does the next stage answer?

6. **Naming**: Save the notebook in the current working directory as `<topic_slug>_guide.ipynb` (e.g., `universal_hashing_guide.ipynb`).

7. **Progress**: After completing the file, print a brief summary of what was generated:
   `Generated <N> stages covering: <stage 0 title> → ... → <final stage title>`

8. **Verify and fix**: After writing the notebook, run this verify-and-fix loop:
   a. Validate JSON structure:
      ```
      python3 -c "import json; json.load(open('<filename>'))"
      ```
      If this fails, fix the JSON and rewrite.
   b. Execute the notebook to verify all code cells run without errors:
      ```
      jupyter nbconvert --to notebook --execute --ExecutePreprocessor.timeout=120 "<filename>" --output "<filename>"
      ```
   c. If execution fails, read the error traceback, fix the broken cell(s) in the notebook, and re-execute. Do not regenerate the entire notebook — only fix what's broken.
   d. Repeat up to 3 times. If it still fails after 3 attempts, save the notebook as-is and tell the user which cell(s) failed and why.

9. **Follow-up suggestions**: After saving, print a brief "What's next?" block with 2-3 contextual follow-up commands using the actual generated filename. For example:

   > **What's next?**
   > - Drill into a stage: `/explore <filename> <stage topic> deeper`
   > - Interrogate a claim: `/explore <filename> <stage topic> why`

   Use the actual generated filename and pick a stage topic from the notebook.

## Example usage

```
/notebook-deep-py universal hashing
/notebook-deep-py B-trees
/notebook-deep-py gradient descent from scratch
/notebook-deep-py how TCP congestion control works
```
