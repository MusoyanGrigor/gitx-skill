# GitX

GitX is a portable Agent Skill for intelligent Git commits and safe pushes.

## Install

```bash
npx skills add MusoyanGrigor/gitx-skill --skill gitx
```

The Skills CLI configures the skill for the selected supported AI agent. Start a new agent session after installation.

## What it does

- Inspects your changes and makes a Conventional Commit.
- When multiple logical commits fit, asks whether to create that number of commits or one commit.
- Can create a `feat/`, `fix/`, or custom-prefixed branch first.
- Pushes safely, asking before it creates a new remote branch.

## Usage

Invoke the installed skill according to your agent's skill interface, then ask it to commit, ship, push, or create a branch and commit.

GitX follows the portable `SKILL.md` Agent Skills format.