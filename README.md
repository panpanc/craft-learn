# CraftLearn

## What it is

CraftLearn is a set of teaching skills that run inside AI coding tools — Claude Code, Codex, Cursor, Windsurf, and others. Every skill starts with motivation, builds intuition before formalism, and layers in complexity through progressive disclosure. The output is files you can run, share, and keep: markdown explanations, interactive Python and TypeScript notebooks, multi-chapter courses, and LeetCode walkthroughs. Every code example is executed and verified before it reaches you.

## Why use this tool to learn?

- **Reason first, recipe second.** Every topic opens with the motivation — so you actually want to keep reading.

- **Get the feel before the formula.** Every concept starts with an analogy or mental model. Formal definitions arrive only after intuition clicks.

- **Crawl, walk, run — in that order.** Every explanation starts simple and layers in complexity only after the foundation clicks.

- **One concept, many contexts.** Every lesson shows how the same idea appears across different problems — so you build transferable understanding, not isolated tricks.

- **No more copy-paste-pray.** Every code example has been run, tested, and proven to work before it shows up in your lesson.

- **See it, don't just read about it.** Lessons generate real graphs, diagrams, and plots — not "imagine a chart here."

## Getting started

### Install

```
git clone https://github.com/panpanc/craft-learn.git
cd craft-learn
```

### Claude Code

Skills in `.claude/skills/` are auto-discovered as slash commands.

```
/learn Milton Friedman's economics ideas as a multi-chapter course
/explain gradient descent
/notebook-deep-py SQL joins
/explore epistemology.md Gettier problem deeper

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

## Learn more

- [Why this beats asking an AI chatbot](WHY.md)
- [Common questions and workflows](QA.md)
