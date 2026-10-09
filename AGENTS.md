# Knot-MCP - Agent Development Guide

Context for AI agents, and people, working on this repository.

## About This Project

Knot-MCP is a planned MCP server shared across Knot installations and users. See the [README](README.md) for what it is meant to do and what is still undecided.

**There is no code yet.** Don't scaffold an implementation, pick a language, or add a build system before a change proposing the server's design has been agreed. That change decides those things.

## Licence boundary

This repository is **MIT**. [Knot-App](https://github.com/pilgrimagesoftware/Knot-App), including its `knot-mcp` crate, is **AGPL-3.0**.

- Don't copy code from Knot-App into this repository.
- Whether Knot-MCP depends on, or takes over, app code is a decision for the server's design change, made with the licensing in view. Don't make it in passing.

## Specs and Changes (OpenSpec)

Work is driven by [OpenSpec](https://github.com/Fission-AI/OpenSpec):

- `openspec/changes/<change>/`: proposals in progress (proposal, design, specs, tasks)
- `openspec/specs/`: the agreed contracts, once a change is archived into them
- `openspec/config.yaml`: project context shown to agents writing artifacts

Use the `openspec-*` skills or the `/opsx:*` commands in `.claude/` to propose, apply and archive changes.

## Committing Code

[Conventional Commits](https://www.conventionalcommits.org/), for example:

```
docs(readme): describe the identity model
feat(server): accept agent registration
docs(openspec): propose the shared server design
```

PRs merge with a **merge commit** so the prefixes survive in history. Don't squash. Commits are signed.

## Branches and Workflow

git-flow. `develop` is the integration branch and the default; `master` is release-only. The meta-repository tracks `develop`.

Make every change in a dedicated `git worktree` on its own feature branch:

- Never commit directly in the primary checkout, which stays on `develop` for syncing and reference.
- Never commit straight to `develop` or `master`.

With the meta-repository checked out, worktrees go under its `Worktrees/` directory, one per branch, prefixed `mcp-`:

```bash
REPO=$(git rev-parse --show-toplevel)   # the Knot-MCP checkout, e.g. <meta>/MCP
git worktree add "$REPO/../Worktrees/mcp-<change>" -b <change> origin/develop
```

`git worktree list` is authoritative for finding the existing ones.

1. Branch from `develop`.
2. Implement against the OpenSpec change.
3. Open a PR to `develop`. Release and hotfix branches PR to `master`.
4. Merge with a merge commit. Delete the merged branch explicitly, rather than with GitHub's automatic deletion, which can't tell a feature branch from a back-merge.

### PR Preflight

- Before committing, confirm `git branch --show-current` is the feature branch, not `develop` or `master`.
- Before opening a PR, confirm the base is `develop`, and that `origin` is `pilgrimagesoftware/Knot-MCP` rather than the meta-repository or Knot-App.
- After opening a PR, verify its base and head with `gh pr view <number> --json baseRefName,headRefName,url`.

## Checks

None yet. CI and a branch ruleset requiring it arrive with the first code.
