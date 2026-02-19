---
name: learn
description: Route learning requests to the best skill based on topic and format signals
---
Route the user's learning request to the best skill. You are a dispatcher — classify the topic, pick the right skill, and invoke it.

## Input

The user provides: $ARGUMENTS

## Step 1: Skill catalog

These are the available skills and their descriptions:

| Skill | Description |
|-------|-------------|
| `explain` | Generate a markdown document that explains a concept through progressive stages |
| `notebook-py` | Generate a Python notebook with illustrative code examples for any topic |
| `notebook-ts` | Generate a Deno notebook with TypeScript code examples for any topic |
| `notebook-deep-py` | Create a deep-dive Python notebook that explains a concept from first principles with illustrative code examples |
| `explore` | Explore a concept from an existing document — go deeper, expand outward, or interrogate claims |
| `leetcode-notebook-py` | Generate a Python notebook that explains a LeetCode problem with interactive solutions |
| `leetcode-notebook-ts` | Generate a Deno notebook with TypeScript code that explains a LeetCode problem with interactive solutions |
| `course-notebook-py` | Generate a multi-chapter notebook course with executable code throughout |
| `course-markdown` | Generate a multi-chapter markdown course that explains with motivation, intuition, and concrete examples |
> **Maintainer note:** Update this table when adding or removing skill files.

**CRITICAL: Only invoke skills from this catalog. Never invoke skills from outside this project (e.g., `frontend-design:*`, `mgrep:*`, `keybindings-help`, or any other external skill).**

## Step 1b: Help mode

If the topic is empty, `--help`, or `--list`, print a concise command reference grouped by category and STOP — do not invoke any skill:

| Category | Commands | Format |
|---|---|---|
| **Explanation** | `explain` | md |
| **Interactive notebook** | `notebook-py`, `notebook-ts`, `notebook-deep-py` | ipynb |
| **Multi-chapter course** | `course-notebook-py`, `course-markdown` | ipynb/md |
| **LeetCode** | `leetcode-notebook-py`, `leetcode-notebook-ts` | ipynb |
| **Follow-up** | `explore` | ipynb/md |

Then show 2-3 quick-start examples:
- `/learn binary search as a notebook`
- `/learn Galois theory from first principles`
- `/learn leetcode 72 edit distance`
- `/learn go deeper on <file>`

## Step 2: Classify by input shape (check in order)

Before topic-matching, check for these structural signals:

### 2a-pre: Selection-based exploration

**Trigger:** Words like "explore the selection", "explore what I copied", "explore what I highlighted", "explore the selected text", "explore from clipboard"

**Steps:**
1. If a file path is explicitly provided, use it directly.
2. If no file path is given, list files in the current working directory (sorted by recency) and find the most recently modified `.md` or `.ipynb` file.
3. Determine the selection source:
   - "copied" / "clipboard" / "pasted" → `--from-clipboard`
   - "selected" / "highlighted" / "selection" → `--from-selection`
4. Route to `explore` with args: `<file_path> --from-clipboard|--from-selection <user's natural language>`

### 2a: Follow-up on existing content

**Trigger:** Words like "go deeper", "deep dive", "expand", "why", "evolve", "improve" AND a reference to an existing file or a concept from recent output.

**Steps:**
1. If a file path is explicitly provided, use it directly.
2. If no file path is given, list files in the current working directory (sorted by recency) and find the most recently modified file whose name matches the topic.
3. Route based on the follow-up verb:
   - "go deeper" / "deep dive" → `explore` with args `<file_path> <concept> deeper`
   - "expand" / "explore variations" → `explore` with args `<file_path> <concept> expand`
   - "why" / "prove it" / "interrogate" → `explore` with args `<file_path> <concept> why`
   - "evolve" / "improve" → `explore` with args `<file_path> <concept> deeper`

### 2b: LeetCode problem

**Trigger:** Arguments contain "leetcode", "LC", a standalone problem number, or a well-known LeetCode problem name.

**Steps:**
1. Determine the variant:
   - If "typescript", "ts", or "deno" is mentioned → `leetcode-notebook-ts`
   - Otherwise → `leetcode-notebook-py`
2. Strip routing keywords and pass the problem identifier as args.

### 2c: Multi-chapter course

**Trigger:** Words like "course", "markdown", "multi-chapter", "full course", "comprehensive course", or a broad topic that clearly spans many sub-topics (e.g., "all of distributed systems", "compiler design end-to-end").

**Steps:**
1. Determine the variant:
   - If "markdown", "textbook", or "book" is mentioned → `course-markdown`
   - Otherwise → `course-notebook-py`
   - If no format preference is stated → **ask the user to choose** between `course-markdown` and `course-notebook-py`
2. Strip routing keywords and pass the topic as args.

## Step 3: Topic-match against discovered skills

If no structural signal matched, match the user's topic against the skill descriptions in the catalog from Step 1.

**How to match:**
1. Compare the user's topic and any modifier words against each skill's first-line description.
2. If a skill's description clearly fits the topic, select it.
3. If the user specified a format preference (e.g., "as a notebook", "markdown", "deep dive"), use that to narrow down among matching skills.
4. If multiple skills could work and the user hasn't specified a format, **ask about their intent** using plain-language questions — NOT command names. Choose from these dimensions as appropriate:

   - **Format**: "Read as prose, or interact with runnable code?"
   - **Depth** (only if code): "Quick overview or deep dive from first principles?"
   - **Scope**: "Single explanation or a multi-chapter course?"
   - **Audience** (if specified): Preserve the audience/level phrase (e.g., "for engineers", "for beginners") and pass it through to the target skill as part of the arguments. Do NOT strip audience phrases — they are content instructions, not routing signals.

   Ask at most 2 questions. Map the answers to the right command:
   - Prose → `explain`
   - Code + quick → `notebook-py`
   - Code + deep → `notebook-deep-py`
   - Course → ask `course-markdown` vs `course-notebook-py`


## Step 4: Invoke

Once you've identified the target skill:
1. Use the **Skill tool** to invoke it with the appropriate arguments.
2. Do NOT add your own explanation — just dispatch. The target skill handles all content generation.

## Examples

| User input | Route | Why |
|---|---|---|
| `binary search` | Ask: prose or code? | No format specified — ask about intent, not command names |
| `binary search as a notebook` | `notebook-py` | "notebook" format signal |
| `binary search as a typescript notebook` | `notebook-ts` | "notebook" + "typescript" format signal |
| `binary search from first principles` | `explain` | "from first principles" matches explain description |
| `leetcode 72 edit distance` | `leetcode-notebook-py` | LeetCode structural signal |
| `leetcode two sum in typescript` | `leetcode-notebook-ts` | LeetCode + "typescript" |
| `Galois theory` | Ask: prose or code? | No format specified — ask about intent |
| `go deeper on collision resolution` | `explore` | Follow-up structural signal (deep-dive mode) |
| `improve hash_tables.md more depth` | `explore` | Follow-up structural signal (deep-dive mode) |
| `distributed systems course` | Ask: markdown or notebook? | "course" trigger, no format specified |
| `compiler design markdown` | `course-markdown` | "markdown" format signal |
| `deep learning course as separate notebooks` | `course-notebook-py` | "course" + "separate notebooks" signal |
| `build a database notebook` | `notebook-deep-py` | Single-notebook progressive format |
| `gradient descent for biologists` | Ask: prose or code? | Audience modifier preserved, no format specified |
| `compiler design course for CS undergrads` | Ask: markdown or notebook? | "course" routes, audience passes through |
