# Local AI Workspace Best Practices

## Problem

When using AI to help build features, requirement screenshots, PRDs, drafts, and tool configs often need to stay local. They are useful for development, but they should not pollute the shared Git repository or be pushed to GitHub by accident.

## Common Bad Patterns

- Adding one-off ignore rules to each project's `.gitignore`
- Letting local AI tool folders appear in `git status`
- Keeping useful requirement material only in temporary local folders with no convention
- Using `assume-unchanged` or `skip-worktree` for untracked local material

## Recommended Setup

Use two layers:

1. Global ignore for cross-project local requirement material
2. Repository-local ignore for AI tool configuration that only matters in one repo

## Global Ignore

Create a global Git ignore file and point Git to it:

```bash
git config --global core.excludesFile ~/.gitignore_global
```

Add a single convention:

```gitignore
.ai-local/
```

Then in any repository you can keep local requirement material like this:

```text
.ai-local/xiaohuangche/
.ai-local/new-feature/
.ai-local/research/
```

Benefits:

- Works in every repository
- No need to keep editing project `.gitignore`
- Easy to tell AI where the source material lives

## Repository-Local Ignore

For tool-specific local config, use `.git/info/exclude` inside the current repository.

Example:

```gitignore
.claude/
```

This keeps the shared repository clean without introducing team-wide ignore rules.

## Good Rules Of Thumb

- Use `.ai-local/` for local requirement material, screenshots, prompts, and drafts
- Use `.git/info/exclude` for repo-specific AI tool folders
- Keep anything team-shared in normal tracked docs, not in local-only folders

## When Not To Use This

Do not hide files that the team must review, maintain, or depend on. Local-only storage is for personal working context, not for project source of truth.

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

If AI needs the material but Git should ignore it, give that material a stable local home. A simple `.ai-local/` convention plus selective use of `.git/info/exclude` is enough for most projects.
