---
name: course-notebook-py
description: Generate a multi-chapter notebook course with executable code throughout
---
Generate a multi-chapter notebook course with executable code throughout.

## Perspective

Explain as a hands-on course designer who:
- Starts every topic with WHY it matters — what problem it solves, what breaks without it
- Builds intuition before formalism — the reader should feel the idea before seeing the code
- Believes understanding comes from running code and seeing results, not just reading
- Thinks in learning arcs — each chapter has a clear purpose in the larger story
- Structures everything as "concept → code → verify → reflect"
- Treats the notebook as a self-paced lab where the reader learns by doing
- Makes every chapter feel like a workshop session — by the end, you've built something
- Treats prerequisites explicitly — the reader always knows what they need before starting a chapter

## Instructions

1. **Parse arguments**: The user provides a topic as: $ARGUMENTS. For example: `"neural networks from scratch"`, `"distributed systems"`, `"compiler design"`.

2. **Design the course**: Plan 5–10 chapters that cover the topic end-to-end. For each chapter, define:
   - **Title**: Clear, descriptive chapter name
   - **Learning objectives**: 2–4 specific things the reader will understand after this chapter
   - **Prerequisites**: Which prior chapters (if any) this depends on
   - **Key concepts**: The 3–5 core ideas covered

   Follow this arc:
   - **Chapters 1–2:** Foundations — the problem space, motivation, key vocabulary, and a compelling demo that gives a taste of the full system
   - **Chapters 3–5:** Core mechanisms — the main ideas, algorithms, or patterns. One major concept per chapter, each producing working code.
   - **Chapters 6–8:** Advanced topics — combine the pieces, handle edge cases, optimizations, trade-offs, real-world considerations
   - **Final chapter(s):** Capstone — a complete working system, benchmarks, and "what we learned"

3. **Preview the syllabus**: Before generating any chapters:
   a. Generate ONLY `00_syllabus.md` in the course directory
   b. Present the syllabus to the user with a summary: chapter count, estimated scope, and the chapter listing
   c. Ask the user: "Does this syllabus look right? You can adjust chapter topics, reorder, add/remove chapters, or change the scope before I generate the full course."
   d. Wait for user confirmation or edits before proceeding
   e. If the user requests changes, update the syllabus and re-present
   f. Once approved, generate all chapters following the finalized syllabus
   g. After writing each chapter file, print a one-line progress update:
      `Written chapter N/M: <chapter_title>`

4. **Generate chapter content**: Each chapter should contain this sequence of cells:

   a. **Chapter header** (markdown): `# Chapter N: Title` with an anchor tag. Include learning objectives and prerequisites for this chapter.
   b. **Motivation** (markdown): 2–3 paragraphs — what problem this chapter solves, why it matters, what we'll build. Connect to the larger course narrative.
   c. **Concept explanation** (markdown): For each key idea, include:
      - **Motivation opener**: 1–2 sentences on why this concept matters here — what problem it solves or what gap it fills
      - **Intuition hook**: An analogy, mental model, or "think of it like..." before the formal explanation
      - Clear explanation building on the intuition, with diagrams (ASCII or described) and LaTeX ($...$) where appropriate
      - Proactively address common misconceptions — name the wrong mental model and explain why it's wrong
   d. **Implementation cells** (3–5 code cells per chapter):
      - Start simple: the most naive version that works
      - Iterate: improve it step by step, explaining each improvement
      - Each code cell produces visible output (prints, asserts, plots)
      - Use small data the reader can trace by hand
      - Include at least one "what goes wrong" cell per major arc — demonstrate the failure case that motivates the correct approach (e.g., the naive solution that times out, the edge case that produces a wrong answer)
      - Where relevant, contrast the current approach with an alternative to highlight trade-offs
   e. **Checkpoint** (code cell): A verification cell that proves the chapter's concept works — a test, a benchmark, or a visualization
   f. **Chapter summary** (markdown): 3–5 bullet takeaways, where this chapter's concept appears in real-world systems, and a bridge to the next chapter

5. **Diagrams and visualizations**: Use matplotlib to make abstract ideas
   concrete. Aim for 2-3 visuals per chapter — not decoration, but
   explanatory tools. Distribute them where they have the most impact:
   - **Early chapters (1-2):** A diagram of the problem space, system
     architecture, or data flow to ground the reader before diving in
   - **Core chapters (3-5):** Step-by-step algorithm traces, before/after
     comparisons, or data structure layouts that make the mechanism visible
   - **Advanced chapters (6+):** Performance curves, benchmark bar charts,
     or architecture diagrams comparing approaches

   When a concept is spatial or structural, a diagram is mandatory — don't
   rely on prose alone. Use simple, labeled plots with clear titles. Prefer
   `plt.figure(figsize=(...))` over defaults for readability.

6. **Connective tissue**: The course should feel like a continuous narrative, not a collection of isolated examples. Use:
   - Callbacks to earlier chapters: "Remember our naive hash function from Chapter 2? Watch what happens..."
   - Foreshadowing: "This will bite us later — we'll fix it in Chapter 5"
   - Running examples: Use the same dataset or problem throughout, showing it from different angles
   - Progressive complexity: Each chapter's code builds on the previous chapter's
   - Cross-references where relevant (e.g., "Recall from Chapter 2 that...")

7. **Closing cells** (after the final chapter):
   - **Capstone summary** (markdown): What we built across the whole course, key design decisions, trade-offs, and the generalizable pattern — what principle transfers beyond this specific topic
   - **Exercises** (markdown): 5–8 extension challenges for the reader, graded by difficulty (easy/medium/hard)
   - **References** (markdown): 3–5 annotated sources

8. **Code style**:
   - Every code cell produces visible output (prints, plots, assertions)
   - Include timing/benchmarking in at least 2 chapters
   - Self-contained — each cell runs after running prior cells (in the same notebook)
   - Standard library + common packages only (numpy, matplotlib, collections, typing, etc.)
   - Type hints throughout
   - Code builds cumulatively — later chapters reuse and extend functions/classes from earlier chapters
   - Comments explain WHY, not WHAT
   - Later chapters can redefine key functions from earlier chapters (include the code inline — don't rely on cross-notebook imports)

## Output format

Generate a `<topic_slug>_course/` directory with a syllabus and one notebook per chapter:

```
<topic_slug>_course/
├── 00_syllabus.md
├── ch01_foundations.ipynb
├── ch02_core_concepts.ipynb
└── ...
```

### Syllabus (`00_syllabus.md`)

Create `00_syllabus.md` in the course directory with:
- Course title and one-paragraph overview
- Prerequisites (what the reader should already know)
- Chapter listing with titles, summaries, and dependency graph
- Suggested reading order (if non-linear paths are possible, mention them)

### Per-chapter notebooks

- **Directory**: Create `<topic_slug>_course/` in the current working directory
- **Per-chapter notebooks**: `ch<NN>_<slug>.ipynb` (e.g., `ch01_foundations.ipynb`)
  - Each notebook opens with a markdown cell stating the chapter title, learning objectives, and prerequisites
  - Each notebook ends with a "What's Next" cell linking to the next chapter
  - Chapters should be self-contained enough to revisit independently, while still cross-referencing prior chapters
- The final chapter notebook includes the closing cells (capstone, exercises, references)

## Verification

After writing each chapter notebook, run this verify-and-fix loop:

1. Validate JSON structure:
   ```
   python3 -c "import json; json.load(open('<filename>'))"
   ```
   If this fails, fix the JSON and rewrite.
2. Execute the notebook to verify all code cells run without errors:
   ```
   jupyter nbconvert --to notebook --execute --ExecutePreprocessor.timeout=120 "<filename>" --output "<filename>"
   ```
3. If execution fails, read the error traceback, fix the broken cell(s) in the notebook, and re-execute. Do not regenerate the entire notebook — only fix what's broken.
4. Repeat up to 3 times per chapter. If it still fails after 3 attempts, save the notebook as-is and tell the user which cell(s) failed and why.
5. Continue to the next chapter regardless — don't let one chapter block the rest.

## Follow-up suggestions

After generating the full course, print a brief "What's next?" block:

> **What's next?**
> - Drill into a chapter concept: `/explore <course_dir>/<chapter_file> <concept> deeper`
> - Expand a section: `/explore <course_dir>/<chapter_file> <section> expand`

Use actual filenames from the generated course.

## Example usage

```
/course-notebook-py neural networks from scratch
/course-notebook-py distributed systems
/course-notebook-py compiler design, focus on the frontend (lexing, parsing, AST)
/course-notebook-py deep learning from scratch using only numpy, no frameworks
/course-notebook-py build a programming language covering lexing through tree-walk interpretation
/course-notebook-py distributed consensus, implement Raft step by step
/course-notebook-py operating systems for backend engineers
```
