---
name: explore
description: Explore a concept from an existing document — go deeper, expand outward, or interrogate claims
---
Explore a concept from an existing document — go deeper, expand outward, or interrogate claims. Infers output format from the input file type.

## Perspective

Explain as an educator who:

- Treats understanding as a zoom lens — each section reveals a new level of detail
- Sees every concept as a node in a larger network of ideas
- Believes nothing should be taken on faith — every claim deserves a "but why?"
- Uses code as both microscope and proof, not just illustration (notebooks) or worked examples and diagrams (markdown)
- Builds on what the reader already knows from the source document

## Instructions

1. **Parse arguments**: The user provides: $ARGUMENTS
   - Format: `<source_path> <concept_or_range> [mode/format keywords] [--from-clipboard|--from-selection]`
   - The first argument is the path to an existing file (markdown, notebook, or text)
   - Everything after the path is the concept or section range
   - Mode and format are detected from natural language (see steps 3-4)
   - Optional input flags: `--from-clipboard`, `--from-selection`
   - Example: `hash_tables.md collision resolution`, `sorting.ipynb quicksort expand`

1b. **Resolve selection input** (if `--from-clipboard` or `--from-selection` is present):

   If `--from-clipboard` is present:
   - Detect platform: run `uname -s` via Bash
   - macOS: run `pbpaste` via Bash to read clipboard contents
   - Linux (WSL): if running under WSL (check for "microsoft" in `uname -r`), run `powershell.exe -command "Get-Clipboard"` via Bash
   - Linux (native): run `xclip -selection clipboard -o` via Bash
   - If none of the above clipboard tools are available, print an error: "No clipboard tool found — install xclip (Linux) or run under macOS/WSL." and STOP.
   - The clipboard text becomes the **concept passage**
   - If the clipboard is empty, print an error: "Clipboard is empty — copy a passage first." and STOP.

   If `--from-selection` is present:
   - Use `mcp__claude-in-chrome__tabs_context_mcp` to get available tabs
   - Use `mcp__claude-in-chrome__javascript_tool` on the active tab to run: `window.getSelection().toString()`
   - The returned text becomes the **concept passage**
   - If the selection is empty, print an error: "No text selected in the browser — highlight a passage first." and STOP.

   For both: after obtaining the passage, read the full source file and locate the passage within it. Use the surrounding section (heading, paragraph context) to identify the concept name for naming and mode detection. If the passage cannot be found verbatim, find the closest matching section.

   The resolved concept passage then replaces the `<concept_or_range>` for all subsequent steps.

2. **Read the source document**: Read the file at the given path. Understand the context around the concept.

3. **Detect mode** from the arguments after the file path:
   - "why", "prove", "interrogate", "justify", "how do we know" → **why**
   - "expand", "broaden", "variations", "compare", "alternatives", "trade-offs" → **expand**
   - "deep dive", "deeper", "go deeper", "under the hood", "mechanics" → **deep-dive**
   - No mode signal → **deep-dive** (default)

4. **Determine output format**:
   - "as notebook", "as a notebook", "with code", "interactive" → `.ipynb` output
   - "as markdown", "as prose", "as a document" → `.md` output
   - Otherwise infer from input file extension:
     - `.md` input → `.md` output
     - `.ipynb` input → `.ipynb` output
     - `.txt` / other → `.md` output (default)

5. **Generate the output** using the mode-specific structure below and the content style matching the output format.

---

## Content style: Notebook (.ipynb)

Apply this style when the output format is `.ipynb`:

- Aim for 1-3 matplotlib visualizations per document — not decoration, but
  explanatory tools. Good candidates:
  - **Internal state traces** (step through an algorithm or data structure operation)
  - **Before/after comparisons** (show the effect of a transformation)
  - **Performance curves or benchmarks** (empirical comparison of approaches)
  - **Architecture or concept diagrams** (how components relate)
- When a concept is spatial or structural, a diagram is mandatory — don't
  rely on prose alone
- Every code cell should produce visible output (prints, plots, or assertions)
- Use small, inspectable data so the reader can trace through results by hand
- Prefer self-contained code — each cell should run independently after running prior cells
- Use only standard library + common packages (numpy, matplotlib, etc.)
- Do not repeat content from the source document — build on it

## Content style: Markdown (.md)

Apply this style when the output format is `.md`:

- Use clear, conversational prose — explain like teaching a colleague
- Include worked examples with specific values the reader can verify by hand
- Use ASCII diagrams and tables where they aid understanding
- Use LaTeX math (inline `$...$` and display `$$...$$`) for formal definitions and derivations
- Include code snippets in fenced blocks only where they clarify implementation details — do not make the document executable
- Do not repeat content from the source document — build on it

---

## Mode: deep-dive

Explore progressively deeper layers of a concept.

Sections:

- **Context Recap**: Brief summary of how the source covers this concept. Orient the reader — "here's what you already know."
- **Why Go Deeper**: What questions remain? What's glossed over? Motivate the dive.
- **Layer 1 — Mechanics**: How does it actually work step by step? (Notebook: code to trace internal behavior with small, concrete data. Markdown: worked example tracing through the algorithm by hand with explicit intermediate values.)
- **Layer 2 — Under the Hood**: Go one level deeper. Data structures, invariants, or mathematical properties. (Notebook: include a matplotlib visualization of internal state. Markdown: ASCII diagram or LaTeX derivation of the key property.)
- **Layer 3 — Edge Cases & Failure Modes**: Where does it break down? What common misconceptions do people have about this concept? (Notebook: code that exposes corner cases and demonstrates why the wrong mental model fails. Markdown: concrete examples of pathological inputs with analysis of why they fail, plus misconceptions addressed explicitly.)
- **Connections Back**: How does this deeper understanding change how you read the original document?
- **Summary & References**: Key insights, common pitfalls to watch for when applying this concept. 2-5 papers/articles/docs for further reading.

---

## Mode: expand

Explore variations, alternatives, and trade-offs around a concept.

Sections:

- **What We Know**: Summarize what the source says. Establish the baseline.
- **Variations & Alternatives**: 2-3 alternative approaches. (Notebook: alternative implementations in code. Markdown: describe each approach with worked examples and trade-off analysis.)
- **Practical Applications**: The concept applied in 2-3 real-world-inspired scenarios. (Notebook: code for each scenario. Markdown: concrete scenarios with analysis.)
- **Comparative Analysis**: Side-by-side comparison. (Notebook: benchmark or compare on the same input, visualize trade-offs with matplotlib. Markdown: comparison table with analysis, ASCII chart if helpful.)
- **Synthesis**: What did expansion reveal? Decision framework for choosing between approaches.
- **Summary & References**: Key trade-offs, common pitfalls to watch for when choosing between approaches. 2-5 papers/articles/docs for further reading.

---

## Mode: why

Interrogate claims Socratically — ask "but why?" and prove each answer.

Sections:

- **Opening**: What the source says about this concept and which 3-5 claims you will examine.
- **[Repeat for each claim]**:
  - **The Claim**: Quote or paraphrase the specific assertion.
  - **But Why?**: Explain why it's true from first principles. (Notebook: code cell demonstrating the underlying principle. Markdown: worked derivation or concrete example.)
  - **Prove It**: Empirical verification. (Notebook: assertions and visible output. Markdown: concrete numerical example with step-by-step verification.)
  - **What If Not?**: Deliberately violate the assumption. Show consequences. (Notebook: code showing wrong answers, degraded performance, crashes; visualize if it makes the failure vivid. Markdown: concrete counterexample with analysis of what goes wrong and why.)
- **So What?**: How do the individual "whys" connect into unified understanding?
- **Summary & References**: Key "whys" distilled, common pitfalls from misunderstanding these principles. 2-5 papers/articles/docs for further reading.

---

## Naming

Use the output format extension determined in step 4:

- deep-dive → `<concept_slug>_deep_dive.<ext>`
- expand → `<concept_slug>_expanded.<ext>`
- why → `<concept_slug>_why.<ext>`

---

## Verify and fix

### Notebook output (.ipynb)

After writing the notebook, run this verify-and-fix loop:

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

### Markdown output (.md)

After writing the document, verify:

a. No unclosed fenced code blocks (every ``` has a matching closing ```)
b. No unclosed LaTeX delimiters (every `$` or `$$` has a matching close)
c. Read the file and fix any issues found.

---

## Follow-up suggestions

After saving, print a brief "What's next?" block with 2-3 suggestions using the actual generated filename. Adapt suggestions to the mode just used:

> **What's next?**
> - Go deeper on a sub-concept: `/explore <filename> <sub-concept> deeper`
> - Interrogate a claim: `/explore <filename> <claim> why`
> - Expand connections: `/explore <filename> <concept> expand`

For example, after a deep-dive suggest expand or why; after expand suggest deeper or challenge.

## Example usage

```
/explore hash_tables.md collision resolution
/explore sorting.ipynb quicksort expand with alternatives
/explore binary_search.ipynb loop invariant — why?
/explore gradient_descent.ipynb learning rate go deeper
/explore epistemology.md Gettier problem deeper
/explore epistemology.md foundationalism as a notebook
/explore epistemology.md --from-clipboard deeper
/explore epistemology.md --from-selection expand
```
