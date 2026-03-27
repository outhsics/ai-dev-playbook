# What Git Worktree Is Actually For: Fewer Clones, Parallel Requirements, Not the Same Branch Everywhere

Chinese version: [git-worktree-vs-clone.zh-CN.md](./git-worktree-vs-clone.zh-CN.md)
Companion article: [multi-ai-branch-and-directory-rules.en.md](./multi-ai-branch-and-directory-rules.en.md)

## Problem

In real projects, people often want to open multiple windows and let multiple AI sessions work in parallel. The immediate questions are usually:

- Can I open the same branch in multiple directories?
- What is the real difference between `git worktree` and multiple `git clone`s?
- How should branches and folders be organized for parallel AI development?

## Context

If multiple AI sessions or editor windows point at the same directory, they are editing the same files. That may look parallel on the surface, but it quickly creates collisions through shared uncommitted changes, shared terminal state, and mixed context.

That is where `git worktree` becomes useful. But it is often misunderstood. It is not a tool for “the same branch in many folders.” It is a tool for “one repository, many working directories, parallel branches.”

## Working Solution

`git worktree` is valuable for two reasons:

1. It reuses the same Git object database instead of forcing a full clone for every task
2. It gives each requirement its own directory and branch for parallel work

It is best understood as:

- a lower-cost alternative to repeated full clones
- an isolation mechanism for parallel requirements on separate branches

It is not:

- a way to check out the same branch in multiple worktrees at the same time
- a safe way for multiple AI sessions to share one branch

## Important Limitation

The most important `git worktree` limitation is this:

one branch can only be checked out by one worktree at a time.

So if `feat/batch-invite-remove-single-import` is already checked out in the main directory, trying to switch another worktree to that same branch will produce an error like:

```text
branch 'feat/batch-invite-remove-single-import' is already checked out at '/path/to/bs-web'
```

That is expected behavior. Git is protecting the branch from being actively edited by multiple worktrees at once.

## When To Use Worktree

Use `git worktree` when:

- one repository needs multiple requirements handled in parallel
- each requirement should live on its own branch
- you want to reduce the cost of repeated full clones
- you want multiple editor windows, each tied to a separate task

A practical rule set is:

- one requirement = one worktree
- one worktree = one branch
- one worktree = one AI session
- one worktree = one editor window

## When To Use Clone

Use repeated `git clone` when you specifically need:

- the same branch open in multiple directories
- fully independent repository copies
- full isolation of Git state, dependency folders, and tool state

If the requirement is “same branch, many directories,” use clones, not worktrees.

## Example

Assume the current repository is `bs-web` and you want to work in parallel on three requirements:

- xiaohuangche
- live coupon
- material upload

```bash
cd /path/to/bs-web

git worktree add ../bs-web-wt-xiaohuangche -b wt/xiaohuangche
git worktree add ../bs-web-wt-live-coupon -b wt/live-coupon
git worktree add ../bs-web-wt-material-upload -b wt/material-upload
```

This gives you:

```text
bs-web/
bs-web-wt-xiaohuangche/
bs-web-wt-live-coupon/
bs-web-wt-material-upload/
```

Those folders can all be opened in separate editor windows, but each worktree stays on its own branch.

## Counterexample

If what you really want is three directories all checked out to `feat/batch-invite-remove-single-import`, then `git worktree` is the wrong tool. Use:

```bash
git clone <repo-url> bs-web-a
git clone <repo-url> bs-web-b
git clone <repo-url> bs-web-c
```

Then switch each clone to the same branch.

## Reusable Rule

The main purpose of `git worktree` is to let one project handle multiple branches and multiple requirements in parallel without paying the cost of a full clone each time.  
If you need the same branch to exist in multiple directories at once, use multiple clones instead of forcing worktrees to do the wrong job.
