---
name: course-markdown
description: Generate a multi-chapter markdown course that explains with motivation, intuition, and concrete examples
---
Generate a multi-chapter markdown course that explains with motivation, intuition, and concrete examples.

## Perspective

Explain as an educator and writer who:
- Starts every topic with WHY it matters — what problem it solves, what breaks without it
- Builds intuition before formalism — the reader should feel the idea before seeing the definition
- Uses concrete examples, analogies, and diagrams to make abstract ideas tangible
- Thinks in learning arcs — each chapter has a clear purpose in the larger story
- Writes prose you'd actually want to read — clear, conversational, never dry
- Treats prerequisites explicitly — the reader always knows what they need before starting a chapter

## Instructions

1. **Parse arguments**: The user provides a topic as: $ARGUMENTS. For example: `"neural networks from scratch"`, `"distributed systems"`, `"compiler design"`.

2. **Design the course**: Plan 5–10 chapters that cover the topic end-to-end. For each chapter, define:
   - **Title**: Clear, descriptive chapter name
   - **Learning objectives**: 2–4 specific things the reader will understand after this chapter
   - **Prerequisites**: Which prior chapters (if any) this depends on
   - **Key concepts**: The 3–5 core ideas covered

   Follow this arc:
   - **Chapters 1–2:** Foundations — the problem space, motivation, key vocabulary, and a compelling example that gives a taste of the full picture
   - **Chapters 3–5:** Core mechanisms — the main ideas, algorithms, or patterns. One major concept per chapter, with worked examples.
   - **Chapters 6–8:** Advanced topics — combine the pieces, handle edge cases, optimizations, trade-offs, real-world considerations
   - **Final chapter(s):** Capstone — synthesis, big picture, open questions, and "what we learned"

3. **Preview the syllabus**: Before generating any chapters:
   a. Generate ONLY `00_syllabus.md` in the course directory
   b. Present the syllabus to the user with a summary: chapter count, estimated scope, and the chapter listing
   c. Ask the user: "Does this syllabus look right? You can adjust chapter topics, reorder, add/remove chapters, or change the scope before I generate the full course."
   d. Wait for user confirmation or edits before proceeding
   e. If the user requests changes, update the syllabus and re-present
   f. Once approved, generate all chapters following the finalized syllabus
   g. After writing each chapter file, print a one-line progress update:
      `Written chapter N/M: <chapter_title>`

4. **Generate chapter content**: Each chapter should contain these sections:

   a. **Chapter header**: `# Chapter N: Title` with learning objectives and prerequisites listed at the top.
   b. **Motivation**: 2–3 paragraphs — what problem this chapter addresses, why it matters, how it fits the larger narrative.
   c. **Concept sections** (2–4 per chapter): Each a `##` heading covering one key idea. Include:
      - **Motivation opener**: 1–2 sentences on why this concept matters here — what problem it solves or what gap it fills in the chapter's narrative
      - **Intuition hook**: An analogy, mental model, or "think of it like..." before the formal explanation
      - Clear prose explanation building on the intuition
      - Diagrams (ASCII art, tables, or described visually) where they aid understanding
      - LaTeX math ($...$) where appropriate
      - Code examples in fenced blocks (```python ... ```) to illustrate concepts — not every section needs code, but use it when it clarifies
      - Worked examples: step through a concrete instance of the concept
      - Misconceptions: proactively address common misunderstandings where relevant
      - Failure cases: include at least one "what goes wrong" worked example per major arc section — show the wrong answer, the timeout, or the subtle bug that motivates the correct approach
      - Where relevant, contrast approaches — show an alternative and explain the trade-offs
      - Verification: include a worked check, proof sketch, or "convince yourself" prompt for at least one key claim per chapter
   d. **Key takeaways**: A boxed or bulleted summary of 3–5 main points, including where this chapter's concept appears in real-world systems
   e. **Chapter summary**: Bridge to the next chapter — what's coming and why it matters

5. **Connective tissue**: The course should feel like a continuous narrative, not a collection of isolated topics. Use:
   - Callbacks to earlier chapters: "Recall from Chapter 2 that..."
   - Foreshadowing: "We'll see why this matters when we reach Chapter 5"
   - Running examples: Return to the same problem from different angles across chapters
   - Progressive depth: Each chapter deepens understanding of the whole
   - Cross-references with chapter numbers (e.g., "see Chapter 3, §Hashing")

6. **Closing sections** (in the final chapter):
   - **Course synthesis**: What we covered across the whole course, key themes, design decisions, trade-offs, and the generalizable pattern — what principle transfers beyond this specific topic
   - **Exercises**: 5–8 extension challenges for the reader, graded by difficulty (easy/medium/hard)
   - **Further reading**: 3–5 annotated references for going deeper

7. **Writing style**:
   - Write in a conversational but precise tone — as if explaining to a smart friend, not lecturing to a classroom
   - Clear, direct prose — explain one thing at a time
   - Code examples in fenced blocks with language tags (e.g., ```python)
   - Include code when it clarifies a concept, but don't force code into every section — some ideas are better explained with prose, diagrams, or math
   - Diagrams and tables are explanatory tools, not decoration. Aim for at least one per chapter. Good candidates:
     - **Architecture or flow diagrams** (ASCII boxes and arrows showing how components connect)
     - **Comparison tables** (side-by-side analysis of approaches, trade-offs, or properties)
     - **State traces** (step-by-step ASCII showing data transformation or algorithm progress)
   - When a concept is spatial or structural, a diagram is mandatory — don't rely on prose alone
   - Use `> **Note:**` blockquotes for important caveats or insights
   - Use `> **Example:**` blockquotes for worked examples
   - Bold key terms on first use
   - Keep paragraphs focused — one idea per paragraph

## Output format

Generate a `<topic_slug>_course/` directory with a syllabus and one markdown file per chapter:

```
<topic_slug>_course/
├── 00_syllabus.md
├── ch01_foundations.md
├── ch02_core_concepts.md
└── ...
```

### Syllabus (`00_syllabus.md`)

Create `00_syllabus.md` in the course directory with:
- Course title and one-paragraph overview
- Prerequisites (what the reader should already know)
- Chapter listing with titles, summaries, and dependency graph
- Suggested reading order (if non-linear paths are possible, mention them)

### Per-chapter files

- **Directory**: Create `<topic_slug>_course/` in the current working directory
- **Per-chapter files**: `ch<NN>_<slug>.md` (e.g., `ch01_foundations.md`)
  - Each file opens with the chapter title, learning objectives, and prerequisites
  - Each file ends with a "What's Next" section linking to the next chapter
  - Chapters should be self-contained enough to revisit independently, while still cross-referencing prior chapters
- The final chapter file includes the closing sections (synthesis, exercises, further reading)

## Follow-up suggestions

After generating the full course, print a brief "What's next?" block:

> **What's next?**
> - Drill into a chapter concept: `/explore <course_dir>/<chapter_file> <concept> deeper`
> - Interrogate a claim: `/explore <course_dir>/<chapter_file> <claim> why`

Use actual filenames from the generated course.

## Example usage

```
/course-markdown neural networks from scratch
/course-markdown distributed systems
/course-markdown compiler design, focus on the frontend (lexing, parsing, AST)
/course-markdown category theory for programmers, not mathematicians
/course-markdown operating systems for backend engineers
/course-markdown database internals covering storage engines through query optimization
```
