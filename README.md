# GitX

GitX is a portable Agent Skill for smart Git commits, branches, checks, previews, and safe pushes.

## Install

```bash
npx skills add MusoyanGrigor/gitx-skill --skill gitx
```

The Skills CLI configures the skill for the selected supported AI agent. Start a new agent session after installation.

## Commands

| Command | Description |
| --- | --- |
| `$gitx` | Inspect changes and create a smart commit. |
| `$gitx body` | Create a smart commit with a useful commit body. |
| `$gitx branch` | Create and switch to a new `hotfix/` branch. |
| `$gitx branch fix/token-refresh` | Create and switch to the named branch. |
| `$gitx branch check` | Create a default branch, run checks, then commit. |
| `$gitx push` | Safely push the current branch. |
| `$gitx check` | Run relevant checks, then create a smart commit. |
| `$gitx status` | Show repository status without changing anything. |
| `$gitx plan` | Preview commit groups and messages without changing anything. |
| `$gitx type fix` | Create a smart commit with the `fix` type. |
| `$gitx scope auth` | Create a smart commit with the `auth` scope. |
| `$gitx files README.md package.json` | Commit only the specified files. |
| `$gitx amend` | Ask before amending the most recent commit. |

If GitX finds several logical commit groups, it asks whether to create the real number of commits or one commit.

## Other agents

Invoke GitX through the agent's skill interface, then use the same command words. For example: `gitx plan`, `gitx check`, or `gitx branch fix/token-refresh`.

GitX follows the portable `SKILL.md` Agent Skills format.