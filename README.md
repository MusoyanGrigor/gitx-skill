# GitX

GitX is a portable Agent Skill for smart Git commits, branches, checks, and safe pushes.

## Install

```bash
npx skills add MusoyanGrigor/gitx-skill --skill gitx
```

The Skills CLI configures the skill for the selected supported AI agent. Start a new agent session after installation.

## Codex Commands

| Command | Description |
| --- | --- |
| `$gitx` | Inspect changes and create a smart commit. |
| `$gitx body` | Create a smart commit with a useful commit body. |
| `$gitx branch` | Create and switch to a new `hotfix/` branch. |
| `$gitx branch fix/token-refresh` | Create and switch to the named branch. |
| `$gitx push` | Safely push the current branch. |
| `$gitx check` | Run relevant checks, then create a smart commit. |

If GitX finds several logical commit groups, it asks whether to create the real number of commits or one commit.

## Other agents

Invoke GitX through the agent's skill interface, then use the same command words. For example: `gitx check` or `gitx branch fix/token-refresh`.

GitX follows the portable `SKILL.md` Agent Skills format.