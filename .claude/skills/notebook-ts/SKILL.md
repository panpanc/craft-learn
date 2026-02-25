---
name: notebook-ts
description: Generate a Deno notebook with TypeScript code examples for any topic
---
Generate a Deno notebook with TypeScript code examples for any topic.

## Perspective

Explain as an educator who:

- Prioritizes "aha moments" over comprehensive coverage
- Uses code as a tool for understanding, not just demonstration
- Builds intuition with analogies before showing the implementation
- Writes for someone who knows programming but not this specific topic

## Instructions

1. **Parse arguments**: The user provides a topic as: $ARGUMENTS. For example:
   `"binary search"`, `"TypeScript generics"`, `"hash tables"`.

2. **Design the notebook** with these 5 sections:

   - **Introduction**: What is this topic? Why does it matter? Include the
     motivation — what problem does it solve? What would we do without it?

   - **Core Concepts**: Break down the key ideas. Build intuition with
     analogies, mental models, or simple diagrams (ASCII art or console.table).
     Explain _why_ things work the way they do, not just _what_ they do.
     Proactively address common misconceptions — name the wrong mental model
     and show why it fails.

   - **Code Examples**: Working TypeScript code that demonstrates each concept.
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

3. **Diagrams and visualizations**: Use inline SVG rendered via
   `Deno.jupyter.display()` to make abstract ideas concrete. Aim for 2-4
   visuals per notebook — not decoration, but explanatory tools. Good
   candidates:
   - **Data structure layouts** (trees, graphs, linked lists, hash tables)
   - **Algorithm step-by-step traces** (highlight the current element, show
     pointers moving)
   - **Before/after comparisons** (e.g., unsorted → sorted)
   - **Performance bar charts** (compare approaches on real data)

   Generate SVG strings programmatically in code cells and display them:
   ```ts
   const svg = `<svg width="400" height="200">...</svg>`;
   Deno.jupyter.display({ "image/svg+xml": svg }, { raw: true });
   ```
   When a concept is spatial or structural, a diagram is mandatory — don't
   rely on prose alone. Keep SVGs simple: labeled rectangles, arrows, and
   text. For tabular comparisons, `console.table` is fine.

4. **Code style**:
   - Every code cell should produce visible output (`console.log`, `console.table`,
     or assertions)
   - Use `console.table` for tabular data where it aids understanding
   - Use small, inspectable data so the reader can trace through results by hand
   - Prefer self-contained code — each cell should run independently after
     running prior cells
   - Use type annotations throughout — leverage TypeScript's type system to
     clarify intent
   - Include at least one verification cell — assert a property, run a sanity
     check, or compare against a known result
   - Use Deno built-ins and the Deno standard library (`https://deno.land/std`)
     when needed — no npm dependencies
   - **Math formatting**: Use LaTeX notation (`$...$` inline, `$$...$$` display) for mathematical formulas in markdown cells — never put math inside fenced code blocks. Reserve code blocks for actual code, ASCII diagrams, and step-by-step computation traces with concrete numbers
   - Do NOT use top-level `export {}` or module wrappers — Deno notebooks run
     cells as scripts

5. **Kernel**: Use the Deno kernel:
   ```json
   "kernelspec": {
     "display_name": "Deno",
     "language": "typescript",
     "name": "deno"
   }
   ```

6. **Naming**: Save the notebook in the current working directory as
   `<topic_slug>_ts.ipynb` (e.g., `binary_search_ts.ipynb`).

7. **Verify and fix**: After writing the notebook, run this verify-and-fix loop:
   a. Validate JSON structure:
      ```
      python3 -c "import json; json.load(open('<filename>'))"
      ```
      If this fails, fix the JSON and rewrite.
   b. Execute the notebook to verify all code cells run without errors:
      ```
      jupyter nbconvert --to notebook --execute --ExecutePreprocessor.timeout=120 --ExecutePreprocessor.kernel_name=deno "<filename>" --output "<filename>"
      ```
   c. If execution fails, read the error traceback, fix the broken cell(s) in the notebook, and re-execute. Do not regenerate the entire notebook — only fix what's broken.
   d. Check markdown cells for LaTeX math (`$...$` or `$$...$$`) inside fenced code blocks. If found, move the math to surrounding markdown prose outside the code block.
   e. Repeat up to 3 times. If it still fails after 3 attempts, save the notebook as-is and tell the user which cell(s) failed and why.

8. **Follow-up suggestions**: After saving, print a brief "What's next?" block with 2-3 contextual follow-up commands using the actual generated filename. For example:

   > **What's next?**
   > - Go deeper on a concept: `/explore <filename> <concept> deeper`
   > - Expand with alternatives: `/explore <filename> <concept> expand`

   Use the actual generated filename and pick a concept from the notebook.

## Example usage

```
/notebook-ts binary search
/notebook-ts TypeScript generics
/notebook-ts hash tables
/notebook-ts recursion and call stacks
```
