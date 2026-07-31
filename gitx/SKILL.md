---
name: gitx
description: "Run the default Smart Git workflow: inspect changes, create one or several logical commits after confirming when several are appropriate, and safely push. Also create a tagged feat/, fix/, or custom-prefixed branch before running Smart when requested. Use for commits, split commits, pushes, shipping work, or branch-first workflows."
---

# GitX

Use one default workflow: **Smart**. Do not present Smart, Split, Ship, or Push as separate choices.

## Smart (default)

Use Smart whenever the user invokes GitX or asks to commit, split commits, push, or ship work.

1. Inspect `git status` and the relevant diff. If file names are supplied, select only those files; otherwise prefer staged changes, then all safe changed files.
2. Include modified tracked files, safe untracked files, and deletions. Exclude ignored files and warn before including risky files.
3. Determine whether the selected changes form one logical commit or multiple logical commit groups.
4. If one commit is appropriate, create one clear Conventional Commit.
5. If two or more commits are appropriate, calculate the number of logical groups and ask exactly:

   > Do you want me to create {count} commits or one commit?

   Create separate Conventional Commits only if the user chooses `{count} commits`; otherwise create one commit.
6. When `--check` is supplied, run relevant checks before committing. If checks fail, ask whether to commit anyway.
7. After committing, use the safe push behavior below. If there are no selected changes and the user asked to push, perform only the push behavior.

Options:

```
--body          # add a useful commit body
--check         # auto-detect and run checks before committing
--scope <name>  # use Conventional Commit scope
--type <type>   # force commit type (fix, feat, docs, test, ...)
```

Examples:

```
GitX
GitX --type fix --scope auth
GitX --check
GitX README.md package.json
```

## Branch first

When the user asks for a branch before committing, create the branch and then run Smart. This is a modifier to Smart, not another mode.

1. Inspect `git status`, `git branch --show-current`, and the working-tree diff.
2. Keep existing changes on the new branch; do not discard or stash them unless the user explicitly asks.
3. Use a valid supplied branch name, or derive a short lowercase kebab-case name. Default prefix: `feat/`; accept `fix/`, `docs/`, `chore/`, `refactor/`, `test/`, or a custom prefix.
4. Check whether the branch exists locally or on `origin`. If it does, ask whether to switch to it or choose another name. Never overwrite it.
5. Create and switch using `git switch -c <branch-name>`, then run Smart.

Examples:

```
GitX branch commit
GitX branch commit fix token refresh
GitX branch commit prefix=hotfix
GitX branch commit name=feature/import-csv
```

## Safe push behavior

1. Push the current branch to `origin` or the configured `push_remote`.
2. If the branch already tracks its remote branch, push it.
3. If it does not yet exist on the remote, ask whether to create it and push with `git push -u <remote> <branch>`.
4. If no remote is configured, say that the local commit was created but nothing was pushed.

## Risky files

Always warn before including likely secrets, credentials, private keys, logs, or build artifacts, including:

```
.env, .env.*
*.pem, *.key
id_rsa, id_ed25519
credentials, token, secret, api_key
debug.log, *.log
dist/, build/, node_modules/
```

## Config file (optional)

`.gitx.yml` is optional. Flags override configuration.

```yaml
gitx:
  default_style: conventional
  push_remote: origin
  checks: opt_in
  include_untracked: true
  include_deleted: true
  secret_warning: basic
```