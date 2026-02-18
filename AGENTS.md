# CraftLearn

A set of agent skills (SKILL.md format) that generate educational content — explanations, notebooks, courses, and LeetCode walkthroughs. Uses the cross-tool SKILL.md standard for portability across Claude Code, Codex CLI, OpenCode, Cursor, Windsurf, and other agents. See [WHY.md](WHY.md) for why this beats asking ChatGPT.

## Getting started

```bash
git clone https://github.com/panpanc/craft-learn.git
cd craft-learn
```

You can either use the **`learn` router** — which picks the best skill based on your topic — or **invoke a specific skill directly** if you already know which one you want.

### Claude Code

Skills in `.claude/skills/` are auto-discovered as slash commands.

**Router:** `/learn <topic>`
**Direct:** `/explain binary search`

### Codex desktop / CLI

Skills are discovered from `.agents/skills/` (symlinked to `.claude/skills/`).

**Router:** `$learn <topic>`
**Direct:** `$notebook-py gradient descent`

### OpenCode

Reads `.claude/skills/` and this file (`AGENTS.md`) automatically.

**Router:** `use the learn skill for <topic>`
**Direct:** `use the leetcode-notebook-py skill for two sum`

### Cursor / Windsurf

Reads `AGENTS.md` as project context.

**Router:** `use the learn skill to teach me about <topic>`
**Direct:** `use the course-notebook-py skill to teach me about transformers`

## Skill structure

`/learn` is the main entry point. It routes to 9 skills based on the topic and format signals:

| Category | Skills | Output |
|---|---|---|
| Explanation | `explain` | .md |
| Interactive notebook | `notebook-py`, `notebook-ts`, `notebook-deep-py` | .ipynb |
| Multi-chapter course | `course-notebook-py` | .ipynb |
| Multi-chapter course | `course-markdown` | .md |
| LeetCode | `leetcode-notebook-py`, `leetcode-notebook-ts` | .ipynb |
| Follow-up | `explore` | .ipynb/.md |

See [QA.md](QA.md) for usage guide and workflows.

## Skills

Skills live as SKILL.md files in the following directories (all equivalent via symlink):

- `.claude/skills/` — primary location
- `.agents/skills/` — symlink, for Codex CLI compatibility

Each skill can be invoked directly (e.g., `/explain binary search`) or via the `/learn` router.
