# CraftLearn

A set of Claude Code skills (SKILL.md format) that generate educational content — explanations, notebooks, courses, and LeetCode walkthroughs. Uses the cross-tool SKILL.md standard for portability across Claude Code, Cursor, Windsurf, and other agents. See [WHY.md](WHY.md) for why this beats asking ChatGPT.

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

All skills live in `.claude/skills/` as SKILL.md files. Each skill can be invoked directly (e.g., `/explain binary search`) or via the `/learn` router.
