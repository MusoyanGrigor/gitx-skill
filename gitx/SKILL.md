---
name: gitx
description: "Run GitX commands for smart commits, commit bodies, branches, checks, and safe pushes. Use when the user asks for gitx, a commit, a branch, checks before committing, or a push."
---

# GitX

Interpret the user request as one GitX command. Do not present separate Smart, Split, or Ship modes.

| Command | Action |
| --- | --- |
| `gitx` | Create a smart commit. |
| `gitx body` | Create a smart commit with a useful commit body. |
| `gitx branch [name]` | Create and switch to a branch. |
| `gitx push` | Safely push the current branch. |
| `gitx check` | Run relevant checks, then create a smart commit. |

## Smart commit

1. Inspect `git status` and the relevant diff. Prefer staged changes; otherwise use all safe changed files.
2. Include modified tracked files, safe untracked files, and deletions. Exclude ignored files and warn before including risky files.
3. Group the selected changes into logical commits.
4. If one commit is appropriate, create one clear Conventional Commit.
5. If two or more commits are appropriate, calculate the real number of logical groups and ask:

   > Do you want me to create N commits or one commit?

   Replace `N` with the real number. Never show `N` or `{count}` literally. Create multiple commits only if the user chooses multiple commits; otherwise create one commit.
6. For `gitx body`, add a useful body to each commit message.
7. Do not push as part of a smart commit. Push only for `gitx push` or when the user explicitly asks to push.

## Branch

For `gitx branch [name]`:

1. Keep existing changes; do not discard or stash them unless the user explicitly asks.
2. Use a valid supplied branch name exactly. If no name is supplied, derive a lowercase kebab-case name and prefix it with `hotfix/`.
3. Check whether the branch exists locally or on `origin`. If it does, ask whether to switch to it or choose another name. Never overwrite it.
4. Create and switch with `git switch -c <branch-name>`.
5. Do not commit or push unless the user also asks.

## Checks

For `gitx check`, detect and run relevant checks such as `npm test`, `npm run lint`, `pnpm test`, `pytest`, `cargo test`, `go test ./...`, or `make test`. If checks fail, ask whether to commit anyway.

## Push

For `gitx push`:

1. Push to `origin` or the configured `push_remote`.
2. If the branch is not on the remote, ask whether to create it and push with `git push -u <remote> <branch>`.
3. If no remote is configured, say that nothing was pushed.

## Risky files

Always warn before including likely secrets, credentials, private keys, logs, or build artifacts, including `.env`, `*.pem`, `*.key`, `credentials`, `token`, `secret`, `api_key`, `*.log`, `dist/`, `build/`, and `node_modules/`.