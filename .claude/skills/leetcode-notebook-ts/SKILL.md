---
name: leetcode-notebook-ts
description: Generate a Deno notebook with TypeScript code that explains a LeetCode problem with interactive solutions
---
Generate a Deno notebook with TypeScript code that explains a LeetCode problem with interactive solutions.

## Perspective

Explain as a problem-solver and educator who:
- Thinks about patterns and transferable techniques, not just solutions
- Values the "aha moment" that makes the solution feel obvious
- Uses code as a tool for understanding, not just demonstration
- Builds intuition with analogies before showing the implementation
- Writes for someone preparing for interviews who wants to understand, not memorize

## Instructions

1. **Parse arguments**: The user provides a problem as: $ARGUMENTS. For example: `"two sum"`, `"LRU cache"`, `"merge intervals"`, `"leetcode 146"`.

2. **Design the notebook** with these sections (each section is a markdown cell followed by one or more code cells where indicated):

   - **Problem** (markdown): Restate the problem clearly. Include input/output format, constraints, and 2-3 example cases.

   - **Intuition** (markdown + code): Why does this approach work? Build understanding with analogies, mental models, or diagrams. Explain the "aha moment" — what insight unlocks the solution? Name the most common wrong intuition about this problem and explain why it fails. Include a code cell that visualizes the idea — use SVG via `Deno.jupyter.display()`, `console.table`, or ASCII art to make the insight visual.

   - **Approach** (markdown): Step-by-step strategy before diving into code. Explain the algorithm in plain English. Mention any data structures used and *why* they're the right choice.

   - **Solution** (code): Working TypeScript solution using LeetCode function signature conventions (standalone functions with proper type annotations). Include a test cases section in the same or following cell that prints results and uses assertions (e.g., `console.assert` or `assertEquals` from Deno std). When showing brute force → optimized, include a cell that demonstrates *why* the brute force fails (e.g., timeout on larger input, wrong answer on a tricky case).

   - **Complexity Analysis** (markdown): Time and space complexity with clear explanations of *why* (not just the Big-O notation).

   - **Edge Cases & Follow-ups** (markdown + code): What edge cases to watch for? Common mistakes? Include a code cell with edge case test assertions. How would the solution change if constraints were different?

   - **Pattern & Generalization** (markdown): What abstract pattern does this problem belong to? (e.g., sliding window, two pointers, monotonic stack). When should you recognize to apply this pattern? Where does this pattern show up outside of interviews (e.g., in databases, networking, OS schedulers)?

   - **Related Problems** (markdown): List 3-5 other LeetCode problems that share similar techniques. For each, briefly explain the connection. Include problem numbers when possible.

   - **Practice Exercises** (markdown + code): 2-3 hands-on variations the reader can try — modify the constraints, change the data structure, or solve a twist on the original problem. Include starter code and hints.

3. **Diagrams and visualizations**: Use inline SVG rendered via
   `Deno.jupyter.display()` to make algorithm behavior visible. Aim for
   1-2 visuals per notebook — not decoration, but tools that build the
   "aha moment." Good candidates:
   - **Algorithm state traces** (array contents at each step, pointer
     positions, window boundaries)
   - **Data structure layouts** (trees, graphs, linked lists, hash maps
     with collision chains)
   - **DP table fills** (show how cells depend on previous cells)
   - **Before/after comparisons** (input → sorted/partitioned/merged output)

   Generate SVG strings programmatically in code cells and display them:
   ```ts
   const svg = `<svg width="400" height="200">...</svg>`;
   Deno.jupyter.display({ "image/svg+xml": svg }, { raw: true });
   ```
   When the problem involves trees, graphs, linked lists, or matrices, a
   diagram is mandatory — don't rely on prose alone. Keep SVGs simple:
   labeled rectangles, arrows, and text. For tabular comparisons,
   `console.table` is fine.

4. **Code style**:
   - Use TypeScript with proper type annotations
   - Follow LeetCode function signature conventions
   - Every code cell should produce visible output (`console.log`, `console.table`, or assertions)
   - Use small, inspectable test data so the reader can trace through results by hand
   - Prefer self-contained code — each cell should run independently after running prior cells
   - Use only Deno built-ins and standard library (no npm specifiers unless necessary)
   - Add comments explaining the *why*, not the *what*

5. **Multiple solutions** (when applicable):
   - If there are multiple approaches (brute force → optimized), show each as a separate code cell
   - Explain the trade-offs between solutions
   - Always include the optimal solution

6. **Notebook metadata**: Set the kernel to Deno in the notebook's `kernelspec` metadata:
   ```json
   "kernelspec": {
     "display_name": "Deno",
     "language": "typescript",
     "name": "deno"
   }
   ```

7. **Naming**: Save the notebook in the current working directory as `<problem_slug>_leetcode_ts.ipynb` (e.g., `two_sum_leetcode_ts.ipynb`).

8. **Verify and fix**: After writing the notebook, run this verify-and-fix loop:
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
   d. Repeat up to 3 times. If it still fails after 3 attempts, save the notebook as-is and tell the user which cell(s) failed and why.

9. **Follow-up suggestions**: After saving, print a brief "What's next?" block with 2-3 contextual follow-up commands using the actual generated filename. For example:

   > **What's next?**
   > - Interrogate the approach: `/explore <filename> <technique> why`
   > - Try a related problem: `/leetcode-notebook-ts <related problem>`

   Use the actual generated filename, pick a technique from the solution, and suggest a related problem from the notebook.

## Example usage

```
/leetcode-notebook-ts two sum
/leetcode-notebook-ts LRU cache
/leetcode-notebook-ts merge intervals
/leetcode-notebook-ts longest substring without repeating characters
/leetcode-notebook-ts leetcode 23 merge k sorted lists
```
