# CraftLearn

## Getting started

### Install

```
git clone https://github.com/panpanc/craft-learn.git
cd craft-learn
```

Then open the project in your preferred AI coding tool:

| Tool | Command |
|------|---------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | `claude` |
| [Codex](https://github.com/openai/codex) | `codex` |
| Cursor / Windsurf / OpenCode | Open the folder in the editor |
### Claude Code

Skills in `.claude/skills/` are auto-discovered as slash commands.

```
/learn Milton Friedman's economics ideas as a multi-chapter course
/explain gradient descent
/notebook-deep-py SQL joins
/explore epistemology.md Gettier problem deeper
/course-markdown quantum mechanics for engineering graduates

```

### Codex

Skills are discovered from `.agents/skills/` (symlinked to `.claude/skills/`).

```
$learn Epistemology as a multi-chapter course
$notebook-py gradient descent
$leetcode-notebook-py coin change
```

### OpenCode

Reads `.claude/skills/` and `AGENTS.md` automatically.

```
use the learn skill for Lie Theory course
```

### Cursor / Windsurf

Reads `AGENTS.md` as project context.

```
use the learn skill to teach me about MinHash algorithm
```

## What it is

CraftLearn is a set of teaching skills that run inside AI coding tools — Claude Code, Codex, Cursor, Windsurf, and others. Every skill starts with motivation, builds intuition before formalism, and layers in complexity through progressive disclosure. The output is files you can run, share, and keep: markdown explanations, interactive Python and TypeScript notebooks, multi-chapter courses, and LeetCode walkthroughs. Every code example is executed and verified before it reaches you.

## Why use this tool to learn?

- **Reason first, recipe second.** Every topic opens with the motivation — so you actually want to keep reading.

- **Get the feel before the formula.** Every concept starts with an analogy or mental model. Formal definitions arrive only after intuition clicks.

- **Crawl, walk, run — in that order.** Every explanation starts simple and layers in complexity only after the foundation clicks.

- **One concept, many contexts.** Every lesson shows how the same idea appears across different problems — so you build transferable understanding, not isolated tricks.

- **No more copy-paste-pray.** Every code example has been run, tested, and proven to work before it shows up in your lesson.

- **See it, don't just read about it.** Lessons generate real graphs, diagrams, and plots — not "imagine a chart here."

## Examples

Browse [`examples/`](examples/) to see what each skill produces. These are real outputs, not mocks.

| Example | Skill | Description |
|---|---|---|
| [Eigenvalues & Eigenvectors](examples/eigenvalues_and_eigenvectors_concept.md) | `explain` | 14-stage explanation from geometric intuition to spectral decomposition and PCA |
| [Epistemology](examples/epistemology/) | `explain` → `explore` | 12-stage explanation + a deep-dive follow-up on coherentism |
| [Gradient Descent](examples/gradient_descent_guide.ipynb) | `notebook-deep-py` | 12-stage deep-dive from slope intuition to Adam optimizer with runnable code |
| [Present Value & Discounting](examples/present_value_and_discounting_guide.ipynb) | `notebook-deep-py` | 13-stage guide from compound interest to bond pricing and DCF analysis |
| [SQL Joins](examples/sql_joins_guide.ipynb) | `notebook-deep-py` | 11-stage guide with Python and SQLite — nested loops to hash joins |
| [Song Writing Course](examples/song_writing_course/) | `course-notebook-py` | 7-chapter notebook course from melody basics to a finished song |
| [Coin Change](examples/coin_change_leetcode.ipynb) | `leetcode-notebook-py` | LeetCode 322 walkthrough — brute force to bottom-up DP with benchmarks and visualizations |
| [Two Sum](examples/two_sum_leetcode.ipynb) | `leetcode-notebook-py` | LeetCode 1 walkthrough — brute force to hash map with animated walkthrough |
| [Hydra Game](examples/hydra_game.ipynb) | `notebook-py` | The Hydra game — tree cutting, regrowth rules, and animated step-by-step walkthrough |

> **Try it yourself:** pick any example and go deeper — `/explore examples/gradient_descent_guide.ipynb momentum deeper`


## Learn more

- [Why this beats asking an AI chatbot](WHY.md)
- [Common questions and workflows](QA.md)

## License

[MIT](https://opensource.org/licenses/MIT)
