---
name: illuminate
description: Illuminate a concept from multiple epistemic angles — historical, foundational, coherentist, perspectival, and across abstraction levels
---
Illuminate a concept by examining it through multiple epistemic lenses. Generate a markdown document that reveals what no single perspective can capture alone.

## Perspective

Write as a philosopher-educator who believes understanding comes from seeing a concept through many lenses. You value:
- Historical arc — how ideas evolved and why
- Mental models — named frameworks that compress insight
- Abstraction levels — the same idea viewed at different altitudes
- Both foundationalist epistemology (build from axioms) and coherentist epistemology (map in a web of beliefs)
- Genuine intellectual tensions and open questions

## Instructions

1. **Parse arguments**: The user provides concepts and an optional source document as: $ARGUMENTS. Multiple concepts can be separated by "and", "vs", or commas (e.g., `"entropy and information"`, `"foundationalism vs coherentism"`). If any argument matches an existing file path, treat it as the source document.

2. **Read source document** (if provided): Read the file and use it as background context. Do not repeat its content — build on it, extend it, and illuminate it from new angles.

3. **Design the document** with these 10 mandatory sections:

   ### a. Opening
   Restate the concept(s), why they matter, and preview the epistemic angles you'll explore. Set the reader's expectations for a multi-lens examination.

   ### b. Historical Arc
   Trace the evolution and development of the concept(s). Name key thinkers and their contributions. Include a timeline or progression showing how understanding shifted over time.

   ### c. Foundational Grounding
   Build the concept from its axioms or first principles (foundationalist approach). What are the bedrock assumptions? What follows logically from them? Show the deductive chain.

   ### d. Web of Connections
   Map the concept within its broader knowledge network (coherentist approach). How does it relate to other ideas? What does it support, and what supports it? Show how believing this concept is justified by its coherence with everything else we know.

   ### e. Multiple Perspectives
   Present 4+ distinct lenses on the concept. Choose from: practitioner, theorist, skeptic, historian, adjacent-field expert, beginner, philosopher, engineer. Each perspective should reveal something the others miss.

   ### f. Mental Models
   Identify 3–5 named mental models that help compress understanding. For each model: name it, explain it, give an example, and note its strengths and limitations.

   ### g. Levels of Abstraction
   Examine the concept at multiple altitudes:
   - **30,000 ft** — the big picture, where it fits in the landscape
   - **10,000 ft** — the key mechanisms and relationships
   - **1,000 ft** — the working details and trade-offs
   - **Ground level** — concrete examples, edge cases, hands-on specifics

   ### h. Related Concepts
   Identify 5–8 adjacent ideas. For each, state the relationship type: "prerequisite", "consequence", "analogy", "tension", "generalization", "special case", "alternative", or "complement".

   ### i. Synthesis
   The payoff — what does the multi-angle examination reveal that no single perspective captures? Name the tensions between perspectives, the surprising connections, and the deeper pattern.

   ### j. Further Exploration
   Pose 5–7 genuine open questions that emerged from this examination. These should be questions worth thinking about, not rhetorical — questions where the multi-angle view exposes gaps or tensions.

4. **Writing style**:
   - Use clear, conversational prose — explain like teaching a thoughtful colleague
   - Prioritize *why we know* and *how we know* over *what* — always surface the epistemology
   - Use LaTeX math (`$...$` / `$$...$$`) where it clarifies formal relationships — never put math inside fenced code blocks. Reserve code blocks for actual code, ASCII diagrams, and step-by-step computation traces with concrete numbers
   - Add ASCII diagrams where they reveal structure
   - Use `> **Insight:**` blockquotes for key revelations that emerge from the multi-angle view
   - Use `> **Tension:**` blockquotes for genuine disagreements or unresolved conflicts between perspectives

5. **Naming**: Save the document in the current working directory as `<concept_slug>_illuminated.md` (e.g., `epistemology_illuminated.md`, `entropy_and_information_illuminated.md`).

6. **Verify**: Before finishing, check for:
   a. All 10 sections (a–j) are present
   b. No unclosed fenced code blocks (every ``` has a matching closing ```)
   c. No unclosed LaTeX delimiters (every `$` or `$$` has a matching close)
   d. No LaTeX math (`$...$` or `$$...$$`) inside fenced code blocks — move any math found in code blocks to surrounding markdown prose
   e. Mental models have both strengths and limitations
   f. At least 4 distinct perspectives in section (e)
   g. Read the file and fix any issues found.

7. **Progress**: After completing the file, print a brief summary:
   `Illuminated <concept(s)> across <N> sections: <section a title> → ... → <section j title>`

8. **Follow-up suggestions**: After saving, print a "What's next?" block:

   > **What's next?**
   > - Explore a thread: `/explore <filename> <concept> deeper`
   > - Illuminate a related concept: `/illuminate <related concept from section h>`

   Use the actual generated filename and pick concepts from the document.

## Example usage

```
/illuminate epistemology
/illuminate entropy and information
/illuminate foundationalism vs coherentism
/illuminate game_theory.md Nash equilibrium and mechanism design
```
