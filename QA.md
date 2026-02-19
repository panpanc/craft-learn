# CraftLearn Q&A

## What skills are available?

| Skill | Output | Description |
|---|---|---|
| `/learn <topic>` | (varies) | Router — classifies your request and dispatches to the right skill |
| `/explain <topic>` | `<slug>.md` | Progressive 8–14 stage explanation built from first principles |
| `/notebook-py <topic>` | `<slug>.ipynb` | Python notebook with code examples and visualizations |
| `/notebook-ts <topic>` | `<slug>_ts.ipynb` | Deno/TypeScript notebook with code examples |
| `/notebook-deep-py <topic>` | `<slug>_guide.ipynb` | Deep-dive Python notebook — naive to production-quality code |
| `/course-markdown <topic>` | `<slug>_course/` dir | Multi-chapter markdown course with syllabus |
| `/course-notebook-py <topic>` | `<slug>_course/` dir | Multi-chapter notebook course with executable code |
| `/leetcode-notebook-py <problem>` | `<slug>_leetcode.ipynb` | Python LeetCode problem walkthrough |
| `/leetcode-notebook-ts <problem>` | `<slug>_leetcode_ts.ipynb` | Deno/TypeScript LeetCode problem walkthrough |
| `/explore <file> <concept>` | `.md` or `.ipynb` | Deep-dive, expand, or interrogate a concept from an existing doc |

---

## Which format should I choose?

- **Prose explanation** — you want to build understanding from first principles, stage by stage. Easy to read and share.
- **Interactive notebook** — you want to run code, see plots, and experiment with parameters.

- **Multi-chapter course** — the topic is broad enough to need multiple connected chapters.
- **LeetCode walkthrough** — you're prepping for interviews and want tested solutions with analysis.

One-liner heuristics:

| If you want... | Use |
|---|---|
| A conceptual explanation from first principles | `explain` |
| Hands-on code you can run | `notebook-py` or `notebook-ts` |
| A progression from naive to production code | `notebook-deep-py` |
| Comprehensive multi-topic coverage | `course-markdown` or `course-notebook-py` |
| Interview prep | `leetcode-notebook-py` or `leetcode-notebook-ts` |
| Content tailored to a specific audience | Add "for \<audience\>" to any command |

---

## Can I specify who the content is for?

Yes. Append your audience or level to any command:

| Example | What it does |
|---|---|
| `/learn SQL joins for backend engineers` | Assumes DB and coding experience, focuses on performance |
| `/explain gradient descent for non-technical managers` | Avoids math, uses business analogies |
| `/course-markdown quantum mechanics for people with undergraduates with rusty calculus and linear algebra` | Refreshes prerequisites as needed |

The skill adapts vocabulary, depth, prerequisites, and examples to match. If you don't specify, the default is a technically literate reader who knows programming but not the specific topic.

---

## What's the difference between notebook-py and notebook-deep-py?

**`notebook-py`** generates a concept explanation with runnable code cells, visualizations, and experiments. The focus is on illustrating and exploring a concept interactively.

**`notebook-deep-py`** follows a naive-to-production progression with code at every stage. You start with a simple (possibly broken) approach and iteratively improve it, learning why each improvement matters.

**When to use each:**
- Use `notebook-py` when you want to explore a concept with code (e.g., `/learn SQL joins as a notebook`).
- Use `notebook-deep-py` when you want to see how a solution evolves from simple to robust.

---

## How do I learn a topic as a notebook?

**Python:**
```
/learn SQL joins as a notebook
```

**TypeScript:**
```
/learn SQL joins as a typescript notebook
```

Both generate `.ipynb` files with runnable code cells, executed and verified before delivery.

---

## How do I build a multi-chapter course?

```
/learn machine learning course
```

The router asks whether you want markdown or notebook format. Then:

1. The skill generates a syllabus and waits for your approval
2. You can add, remove, or reorder chapters before generation starts
3. Each chapter references earlier material and foreshadows later topics
4. The full course is generated into a `<topic>_course/` directory

---

## How does the router decide which skill to use?

The router checks your input in this priority order:

1. **Help mode** — empty input, `--help`, or `--list` prints the skill catalog
2. **Selection-based exploration** — "explore the selection" or "explore what I copied"
3. **Follow-up on existing content** — "go deeper", "expand", "why", "improve" + a file reference
4. **LeetCode** — "leetcode", "LC", a problem number, or a known problem name
5. **Multi-chapter course** — "course", "multi-chapter", "full course", or a broad multi-topic subject
6. **Topic matching** — compares your topic against skill descriptions; asks clarifying questions if ambiguous

When multiple skills could fit and you haven't specified a format, the router asks plain-language questions:

- **Format**: "Read as prose, or interact with runnable code?"
- **Depth** (only if code): "Quick overview or deep dive from first principles?"
- **Scope**: "Single explanation or a multi-chapter course?"

---

## What are some example commands?

| Input | Routes to | Why |
|---|---|---|
| `SQL joins` | Asks: prose or code? | Ambiguous — no format specified |
| `SQL joins as a notebook` | `notebook-py` | "notebook" format signal |
| `SQL joins as a typescript notebook` | `notebook-ts` | "notebook" + "typescript" |
| `gradient descent from first principles` | `explain` | "from first principles" matches explain |
| `leetcode 322 coin change` | `leetcode-notebook-py` | LeetCode structural signal |
| `leetcode two sum in typescript` | `leetcode-notebook-ts` | LeetCode + "typescript" |
| `go deeper on collision resolution` | `explore` (deep-dive) | Follow-up signal |
| `improve sql_joins.ipynb more depth` | `explore` (deep-dive) | Follow-up signal with file |
| `machine learning course` | Asks: markdown or notebook? | "course" trigger, no format |
| `compiler design markdown` | `course-markdown` | "markdown" format signal |
| `gradient descent for biologists` | `explain` | Audience signal doesn't change routing — just adapts content |
| `quantum mechanics course for engineers` | Asks: markdown or notebook? | Audience passes through to the chosen skill |

---

## I already generated a doc — how do I go deeper?

Use `/explore` to build on any generated file:

```
/explore <file> <concept> deeper    # deep-dive into a specific concept
/explore <file> <concept> expand    # broaden coverage of a concept
/explore <file> <concept> why       # interrogate claims and assumptions
```

Example chain starting from SQL joins:

```
/learn SQL joins                                     # generates sql_joins.md
/explore sql_joins.md performance deeper      # generates performance_deep_dive.md
/explore sql_joins.md when to denormalize why
                                                     # generates denormalize_why.md
```

Each follow-up reads the original document and builds on it — the deeper explanation knows what was already covered.

---

## What files does each skill create?

| Skill | Filename pattern |
|---|---|
| `explain` | `<topic_slug>.md` |
| `notebook-py` | `<topic_slug>.ipynb` |
| `notebook-ts` | `<topic_slug>_ts.ipynb` |
| `notebook-deep-py` | `<topic_slug>_guide.ipynb` |
| `course-markdown` | `<topic_slug>_course/` (dir with `00_syllabus.md` + `ch<NN>_<slug>.md`) |
| `course-notebook-py` | `<topic_slug>_course/` (dir with `00_syllabus.md` + `ch<NN>_<slug>.ipynb`) |
| `leetcode-notebook-py` | `<problem_slug>_leetcode.ipynb` |
| `leetcode-notebook-ts` | `<problem_slug>_leetcode_ts.ipynb` |
| `explore` | `<concept_slug>_deep_dive|_expanded|_why.<ext>` |

---

## Can I use this in Cursor, Windsurf, or other tools?

Yes. Skills use the [SKILL.md standard](https://code.claude.com/docs/en/skills) for portability.

| Tool | Skills directory | Instructions file | Setup |
|------|-----------------|-------------------|-------|
| **Claude Code** | `.claude/skills/` | `CLAUDE.md` | Works out of the box |
| **OpenAI Codex CLI** | `.agents/skills/` | `AGENTS.md` | Works out of the box (symlink provided) |
| **OpenCode** | `.claude/skills/` | `AGENTS.md` | Works out of the box |
| **Cursor** | — | `AGENTS.md` | Works out of the box |
| **Windsurf** | — | `AGENTS.md` | Works out of the box |

**Directory layout:**

```
.claude/skills/      ← primary location (1 router + 9 skill directories, each with SKILL.md)
.agents/skills/      ← symlink → ../.claude/skills (for Codex CLI)
CLAUDE.md            ← Claude Code project instructions
AGENTS.md            ← cross-tool project instructions (Codex, OpenCode, Cursor, Windsurf)
```

---

## Workflows

### Explanation → deep-dive → interrogate

Build understanding from first principles, then drill into what interests you.

```
/learn gradient descent from first principles
                                              # → explain → gradient_descent.md

/explore gradient_descent.md momentum deeper
                                              # → momentum_deep_dive.md

/explore gradient_descent.md convergence why
                                              # → convergence_why.md
```

### Interactive notebook → expand → deep-dive

Interactive learning with iterative refinement.

```
/learn SQL joins as a notebook
                                              # → notebook-py → sql_joins.ipynb

/explore sql_joins.ipynb subquery performance expand
                                              # → subquery_performance_expanded.ipynb

/explore sql_joins.ipynb hash joins deeper
                                              # → hash_joins_deep_dive.ipynb
```

### Full course workflow

For comprehensive coverage of a broad topic.

```
/learn machine learning course
                                              # Router asks: markdown or notebook?
                                              # You pick: notebook
                                              # → course-notebook-py previews syllabus, waits for approval
                                              # → generates machine_learning_course/ with all chapters

/explore machine_learning_course/ch03_neural_networks.ipynb backpropagation deeper
                                              # → backpropagation_deep_dive.ipynb

/explore machine_learning_course/ch05_regularization.ipynb dropout vs weight decay expand
                                              # → dropout_vs_weight_decay_expanded.ipynb
```

### Explore from clipboard

Copy a passage from any source (blog post, textbook, docs), then explore it in the context of a file you've already generated.

```
# 1. Generate a document
/learn hash tables as a notebook
                                              # → notebook-py → hash_tables.ipynb

# 2. Copy a passage to your clipboard (e.g., from a blog post about Robin Hood hashing)

# 3. Explore it in context of your file
/explore hash_tables.ipynb --from-clipboard deeper
                                              # → robin_hood_hashing_deep_dive.ipynb

# 4. Or use natural language through the router
/learn explore what I copied
                                              # auto-finds most recent .md/.ipynb, reads clipboard
                                              # → explore (deep-dive by default)
```

The clipboard text is matched against the source file to find surrounding context. You can combine `--from-clipboard` with any mode:

```
/explore hash_tables.ipynb --from-clipboard expand
/explore hash_tables.ipynb --from-clipboard why
```

### LeetCode practice

```
/learn leetcode 322 coin change
                                              # → leetcode-notebook-py → coin_change_leetcode.ipynb

/explore coin_change_leetcode.ipynb dynamic programming table why
                                              # → dynamic_programming_table_why.ipynb

/learn leetcode two sum in typescript
                                              # → leetcode-notebook-ts → two_sum_leetcode_ts.ipynb
```
