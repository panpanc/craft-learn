---
name: leetcode-notebook-py
description: Generate a Python notebook that explains a LeetCode problem with interactive solutions
---
Generate a Python notebook that explains a LeetCode problem with interactive solutions.

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

   - **Intuition** (markdown + code): Why does this approach work? Build understanding with analogies, mental models, or diagrams. Explain the "aha moment" — what insight unlocks the solution? Name 2-3 common wrong approaches — for each, explain what it tries, why it seems reasonable, and exactly why it fails (wrong answer, TLE, or missing edge case). Include a code cell with a visualization (matplotlib or ASCII) that shows the problem structure — the "aha" diagram that makes the insight visual (e.g., visualizing array state, tree structure, or algorithm progression).

   - **Approach** (markdown): Step-by-step strategy before diving into code. Explain the algorithm in plain English. Mention any data structures used and *why* they're the right choice.

   - **Solution** (code): Working Python solution using LeetCode conventions (`class Solution`, type hints with `List[int]`, `Optional[TreeNode]`, etc.). Include a test cases section in the same or following cell that prints results and uses assertions. When multiple approaches exist, show the full progression as separate Solution cells (e.g., O(n²) → O(n log n) → O(n)). For each step: implement it, demo it working on examples, then demo the limitation that motivates the next step (e.g., timeout on larger input, wrong answer on a tricky case). Include a visualization in a code cell that traces the algorithm state on an example (e.g., pointer positions, window boundaries, hash map contents at each iteration).

   - **Walkthrough** (code, after each Solution cell): Trace through one example input step by step, printing variable state at each iteration (loop counter, pointer positions, data structure contents, decisions made). This is how interviewers expect candidates to verify — "walk me through this."

   - **Benchmark** (code): Run both brute force and optimal solutions on increasing input sizes (e.g., n = 100, 1000, 5000, 10000), print a timing table, and plot the performance curves using matplotlib. Makes Big-O tangible — the reader sees O(n²) vs O(n) as real seconds, not just notation.

   - **Complexity Analysis** (markdown): Time and space complexity with clear explanations of *why* (not just the Big-O notation).

   - **Edge Cases & Follow-ups** (markdown + code): What edge cases to watch for? Common mistakes? Include a code cell with edge case test assertions. How would the solution change if constraints were different?

   - **Pattern & Generalization** (markdown): What abstract pattern does this problem belong to? (e.g., sliding window, two pointers, monotonic stack). When should you recognize to apply this pattern? Name 1-2 scenarios where this pattern seems applicable but doesn't work, and which pattern to use instead — this prevents over-application in interviews. Where does this pattern show up outside of interviews (e.g., in databases, networking, OS schedulers)?

   - **Related Problems** (markdown): List 3-5 other LeetCode problems that share similar techniques. For each, briefly explain the connection. Include problem numbers when possible.

   - **Practice Exercises** (markdown + code): 2-3 hands-on variations the reader can try — modify the constraints, change the data structure, or solve a twist on the original problem. Include starter code and hints.

3. **Diagrams and visualizations**: Use matplotlib to make algorithm
   behavior visible. Aim for 2-3 visuals per notebook — not decoration, but
   tools that build understanding. Distribute them where they have the most
   impact:
   - **Intuition section:** Problem structure visualization — the "aha"
     diagram that makes the insight click (e.g., data structure layout,
     problem space, why the naive approach fails visually)
   - **Solution section:** Algorithm state trace on an example (array
     contents at each step, pointer positions, window boundaries, DP table
     fill showing cell dependencies)
   - **Benchmark section:** Performance comparison chart (timing curves
     for brute force vs optimal on increasing input sizes)

   When the problem involves trees, graphs, linked lists, or matrices, a
   diagram is mandatory — don't rely on prose alone. Use simple, labeled
   plots with clear titles. Prefer `plt.figure(figsize=(...))` over
   defaults for readability.

4. **Code style**:
   - Use Python with type hints (from `typing` module)
   - Follow LeetCode `class Solution` conventions
   - Every code cell should produce visible output (prints or assertions)
   - Use small, inspectable test data so the reader can trace through results by hand
   - Prefer self-contained code — each cell should run independently after running prior cells
   - Use only standard library + common packages (typing, collections, heapq, matplotlib, etc.)
   - Add comments explaining the *why*, not the *what*

5. **Multiple solutions** (when applicable):
   - Show the full progression as separate Solution cells (e.g., O(n²) → O(n log n) → O(n))
   - For each approach: implement → demo working → demo limitation → transition to next
   - Follow each Solution cell with a Walkthrough cell tracing one example step by step
   - Explain the trade-offs between solutions
   - Always include the optimal solution

6. **Naming**: Save the notebook in the current working directory as `<problem_slug>_leetcode.ipynb` (e.g., `two_sum_leetcode.ipynb`).

7. **Verify and fix**: After writing the notebook, run this verify-and-fix loop:
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

8. **Follow-up suggestions**: After saving, print a brief "What's next?" block with 2-3 contextual follow-up commands using the actual generated filename. For example:

   > **What's next?**
   > - Interrogate the approach: `/explore <filename> <technique> why`
   > - Try a related problem: `/leetcode-notebook-py <related problem>`

   Use the actual generated filename, pick a technique from the solution, and suggest a related problem from the notebook.

## Example usage

```
/leetcode-notebook-py two sum
/leetcode-notebook-py LRU cache
/leetcode-notebook-py merge intervals
/leetcode-notebook-py longest substring without repeating characters
/leetcode-notebook-py leetcode 23 merge k sorted lists
```
