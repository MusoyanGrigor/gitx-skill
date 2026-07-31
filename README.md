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

## Commands

After invoking GitX through your AI agent's skill interface, you can ask it to:

- **Smart commit:** “Commit my changes.”
- **Branch + commit:** “Create a `feat/` branch and commit these changes.”
- **Fix branch:** “Create a `fix/token-refresh` branch, then commit.”
- **Custom branch prefix:** “Create a `hotfix/` branch and commit.”
- **Push:** “Push my current branch.”
- **Check before committing:** “Commit my changes and run checks first.”

GitX inspects the changes automatically. If it identifies multiple logical commits, it asks:

> Do you want me to create {count} commits or one commit?

### Codex example

```text
$gitx
$gitx branch commit fix token refresh
$gitx --check
```

GitX follows the portable `SKILL.md` Agent Skills format.