# Branch and Directory Rules for Parallel AI Development

Chinese version: [multi-ai-branch-and-directory-rules.zh-CN.md](./multi-ai-branch-and-directory-rules.zh-CN.md)
Companion article: [git-worktree-vs-clone.en.md](./git-worktree-vs-clone.en.md)

## Problem

Once a project starts handling multiple requirements in parallel and different AI sessions are asked to work at the same time, the real risk is usually not the code itself. The real risk is missing rules for branches and directories.

Typical failure modes include:

- multiple AI sessions editing the same directory
- multiple requirements sharing one branch
- many editor windows that still point to the same working copy
- requirement notes, temporary instructions, and commit history getting mixed together

## Context

Many teams adopt AI by solving only the first question: “can AI write code here?” They do not solve the second question: “how do multiple AI sessions work safely in parallel?”

Without explicit structure, parallel AI development usually leads to:

- overwritten changes
- mixed context
- messy commit history
- unclear ownership during merge
- AI continuing work in the wrong directory

So the real need is not “more windows.” It is a simple, durable branch-and-directory convention.

## Working Solution

The most practical default rule set is:

1. one requirement = one directory
2. one requirement = one branch
3. one directory = one AI session
4. one directory = one primary editor window

If the project is already in Git, `git worktree` is usually the best directory-level isolation mechanism.

## Recommended Directory Rules

Keep the main repository directory for the main line or primary feature branch.  
Use sibling directories for parallel requirements with a consistent naming pattern.

For example:

```text
bs-web/
bs-web-wt-xiaohuangche/
bs-web-wt-live-coupon/
bs-web-wt-material-upload/
```

Good defaults:

- the main directory handles the main line only
- parallel directories use a `*-wt-*` pattern
- directory names describe the requirement directly

## Recommended Branch Rules

Do not keep piling unrelated work into one generic branch name.

A better pattern is:

- one primary branch for the main feature line
- one child branch per parallel requirement

For example:

```text
feat/batch-invite-remove-single-import
wt/xiaohuangche
wt/live-coupon
wt/material-upload
```

If you want more explicit names, this works well too:

```text
feat/batch-invite/xiaohuangche
feat/batch-invite/live-coupon
feat/batch-invite/material-upload
```

The important part is not the prefix. The important part is that each parallel requirement gets its own branch.

## AI Operating Rules

For AI sessions, speed matters less than staying in the correct workspace.

Useful default rules are:

1. confirm the current directory before editing
2. confirm the current branch before editing
3. only work on the requirement assigned to this worktree
4. do not casually modify files for another active requirement
5. keep local-only requirement material under this directory's `.ai-local/`

For example:

```text
.ai-local/xiaohuangche/
.ai-local/live-coupon/
```

## Commit Rules

Parallel development makes commit discipline more important than usual.

Recommended defaults:

- each requirement commits only its own changes
- do not mix multiple requirements into one commit
- let the commit message reflect the requirement clearly
- review on the branch before merging back

## What Not To Do

These patterns are risky in multi-AI development:

- multiple AI sessions sharing one directory
- multiple AI sessions sharing one branch
- handling several requirements casually from one workspace
- letting AI start work without checking path and branch first

They may feel faster in the moment, but they almost always damage context boundaries, commit clarity, and merge safety later.

## Minimal Example

```bash
git worktree add ../bs-web-wt-xiaohuangche -b wt/xiaohuangche
git worktree add ../bs-web-wt-live-coupon -b wt/live-coupon
git worktree add ../bs-web-wt-material-upload -b wt/material-upload
```

Then:

- one window opens `bs-web-wt-xiaohuangche`
- one window opens `bs-web-wt-live-coupon`
- one window opens `bs-web-wt-material-upload`
- each window is assigned to exactly one AI session

## Reusable Rule

In parallel AI development, manage directories and branches before managing code.  
The safest default is simple: one requirement, one directory, one branch, one AI.
