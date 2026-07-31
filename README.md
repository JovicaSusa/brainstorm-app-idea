# brainstorm-app-idea

A [Claude Code](https://claude.com/claude-code) skill that runs a structured
brainstorming session for a rough app idea: competitive research, adaptive
clarifying questions, and a three-perspective (Champion / Advisor / Investor)
critique — ending with a saved markdown write-up of the whole session.

## Install

Copy `SKILL.md` into a `brainstorm-app-idea/` folder under your Claude Code
skills directory:

```bash
mkdir -p ~/.claude/skills/brainstorm-app-idea
cp SKILL.md ~/.claude/skills/brainstorm-app-idea/SKILL.md
```

## Use

In Claude Code:

```
/brainstorm-app-idea <your rough app idea>
```
