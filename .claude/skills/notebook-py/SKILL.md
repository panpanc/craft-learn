---
name: notebook-py
description: Generate a Python notebook with illustrative code examples for any topic
---
Generate a Python notebook with illustrative code examples for any topic.

## Perspective

Explain as an educator who:

- Prioritizes "aha moments" over comprehensive coverage
- Uses code as a tool for understanding, not just demonstration
- Builds intuition with analogies before showing the implementation
- Writes for someone who knows programming but not this specific topic

## Instructions

1. **Parse arguments**: The user provides a topic as: $ARGUMENTS. For example:
   `"binary search"`, `"Python decorators"`, `"hash tables"`.

2. **Design the notebook** with these 5 sections:

   - **Introduction**: What is this topic? Why does it matter? Include the
     motivation — what problem does it solve? What would we do without it?

   - **Core Concepts**: Break down the key ideas. Build intuition with
     analogies, mental models. Explain
     _why_ things work the way they do, not just _what_ they do. Proactively
     address common misconceptions — name the wrong mental model and show why
     it fails.

   - **Code Examples**: Working Python code that demonstrates each concept.
     Start simple and build complexity. Each example should reinforce the
     intuition from the previous section. Include at least one "what happens
     when this goes wrong" cell — demonstrate the failure case that motivates
     the correct approach. Where relevant, contrast with an alternative approach
     to highlight trade-offs.

   - **Summary**: Key takeaways, common pitfalls to avoid, when this approach
     does *not* apply, where this shows up in real-world systems, the
     transferable principle (what generalizes beyond this topic), and
     suggestions for what to explore next. End with 2-3 practice exercises
     the reader can try.

   - **References**: List 2-5 papers, articles, or official documentation for
     further reading. For each, include the title, author/source, and a one-line
     description of what it covers. Prioritize seminal papers, authoritative
     tutorials, and accessible explanations.

3. **Diagrams and visualizations**: Use matplotlib to make abstract ideas
   concrete. Aim for 2-4 visuals per notebook — not decoration, but
   explanatory tools. Good candidates:
   - **Before/after comparisons** (e.g., unsorted → sorted, unbalanced → balanced)
   - **Data structure layouts** (trees, graphs, linked lists, hash tables)
   - **Algorithm step-by-step traces** (highlight the current element, show
     pointers moving)
   - **Performance curves** (O(n) vs O(log n) on real data)
   - **Concept maps** (how components relate to each other)

   When a concept is spatial or structural, a diagram is mandatory — don't
   rely on prose alone. Use simple, labeled plots with clear titles. Prefer
   `plt.figure(figsize=(...))` over defaults for readability.

4. **Code style**:
   - Every code cell should produce visible output (prints, plots, or
     assertions)
   - Use small, inspectable data so the reader can trace through results by hand
   - Prefer self-contained code — each cell should run independently after
     running prior cells
   - Include at least one verification cell — assert a property, run a sanity
     check, or benchmark against a known result
   - Use only standard library + common packages (numpy, matplotlib, etc.)
   - Highlight key insights and "aha moments" explicitly — use markdown cells to call out the crucial realization
   - End each section with a brief transition to the next — what question does the next section answer?

5. **Naming**: Save the notebook in the current working directory as
   `<topic_slug>.ipynb` (e.g., `binary_search.ipynb`).

6. **Verify and fix**: After writing the notebook, run this verify-and-fix loop:
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

7. **Follow-up suggestions**: After saving, print a brief "What's next?" block with 2-3 contextual follow-up commands using the actual generated filename. For example:

   > **What's next?**
   > - Go deeper on a concept: `/explore <filename> <concept> deeper`
   > - Expand with alternatives: `/explore <filename> <concept> expand`

   Use the actual generated filename and pick a concept from the notebook.

## Example usage

```
/notebook-py binary search
/notebook-py Python decorators
/notebook-py hash tables
/notebook-py recursion and call stacks
```
