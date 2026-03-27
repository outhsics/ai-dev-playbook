# Local AI Workspace Best Practices

Chinese version: [local-ai-workspace.zh-CN.md](./local-ai-workspace.zh-CN.md)

## Problem

When using AI to help with development, requirement screenshots, PRDs, research material, drafts, and tool configs often need to stay local. They are useful for development, but they should not pollute the shared repository or be pushed to GitHub by accident.

## Common Bad Patterns

- adding one-off rules to each project's `.gitignore`
- letting local AI tool folders keep showing up in `git status`
- keeping useful requirement material in scattered temporary folders with no convention
- using `assume-unchanged` or `skip-worktree` for untracked local material

## Recommended Setup

Use two layers:

1. global ignore for cross-project local material
2. repository-local ignore for AI tool config that only matters in one repo

## Global Ignore

Create a global Git ignore file:

```bash
git config --global core.excludesFile ~/.gitignore_global
```

Add one shared convention:

```gitignore
.ai-local/
```

Then any repository can keep local material like this:

```text
.ai-local/xiaohuangche/
.ai-local/new-feature/
.ai-local/research/
```

Benefits:

- works across repositories
- no repeated project `.gitignore` edits
- easier to tell AI where the source material lives

## Repository-Local Ignore

For tool-specific local config, use `.git/info/exclude` inside the current repository.

Example:

```gitignore
.claude/
```

This keeps the repository clean without introducing team-wide ignore rules.

## Rules Of Thumb

- use `.ai-local/` for local requirement material, screenshots, prompts, and drafts
- use `.git/info/exclude` for repo-specific AI tool folders
- keep team-shared source-of-truth docs as normal tracked files

## When Not To Use This

Do not hide files that the team must review, maintain, or depend on in local-only folders.

## Minimal Example

```text
my-project/
  .ai-local/
    xiaohuangche/
    feature-b-brief/
  .claude/
  src/
  package.json
```

## Takeaway

If AI needs the material but Git should ignore it, give that material a stable local home. For most projects, a simple `.ai-local/` convention plus selective use of `.git/info/exclude` is enough.
