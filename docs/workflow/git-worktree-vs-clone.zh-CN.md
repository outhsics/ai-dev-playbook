# Git Worktree 的真正用途：少 Clone、并行多需求，但不要共用同一分支

English version: [git-worktree-vs-clone.en.md](./git-worktree-vs-clone.en.md)

## 问题

做一个项目时，常见需求是同时开多个窗口、让多个 AI 并行处理不同任务。很多人第一反应是：

- 能不能在不同目录里同时打开同一个分支？
- `git worktree` 和多次 `git clone` 到底有什么区别？
- 多个 AI 并行开发时，应该怎么组织目录和分支？

## 背景

如果多个 AI 或多个编辑器窗口都指向同一个目录，大家其实在改同一套文件。这样虽然“看起来”是并行，但很容易互相覆盖、共享未提交改动、共享终端状态，最后把上下文和改动搅在一起。

这时 `git worktree` 经常被拿出来讨论，但它不是“同一个分支多开几份”的工具，而是“一个仓库、多套工作目录、多个分支并行”的工具。

## 有效解法

`git worktree` 的核心价值有两点：

1. 复用同一个 Git 仓库对象库，不需要为每个任务完整 clone 一份仓库
2. 给不同需求提供独立目录和独立分支，适合并行开发

它更像是：

- 节省磁盘和 clone 时间的多工作目录方案
- 给并行需求做隔离的分支工作台

而不是：

- 同一个分支在多个目录里同时签出
- 多个 AI 安全地共用同一条分支

## 关键限制

`git worktree` 有一个经常让人误解的限制：

同一个分支，同一时刻只能被一个 worktree 签出。

所以如果 `feat/batch-invite-remove-single-import` 已经在主目录里签出，再去另一个 worktree 里切这个分支，就会看到类似提示：

```text
branch 'feat/batch-invite-remove-single-import' is already checked out at '/path/to/bs-web'
```

这不是异常，而是 Git 用来避免同一分支在多个工作树里被同时修改的保护机制。

## 什么时候该用 Worktree

适合这些场景：

- 一个项目里并行处理多个需求
- 每个需求都应该有独立分支
- 想减少重复 clone 的成本
- 需要同时开多个编辑器窗口，但每个窗口对应不同任务

推荐规则：

- 一个需求 = 一个 worktree
- 一个 worktree = 一个分支
- 一个 worktree = 一个 AI
- 一个 worktree = 一个编辑器窗口

## 什么时候该用 Clone

如果你的目标是：

- 在不同目录里同时打开同一个分支
- 同时保留多份完全独立的仓库副本
- 需要把 Git 配置、依赖目录、工具状态也完全隔离

那就应该用多次 `git clone`，而不是 `git worktree`。

## 示例

假设当前仓库是 `bs-web`，你想并行处理小黄车、直播优惠券、素材上传三个需求：

```bash
cd /path/to/bs-web

git worktree add ../bs-web-wt-xiaohuangche -b wt/xiaohuangche
git worktree add ../bs-web-wt-live-coupon -b wt/live-coupon
git worktree add ../bs-web-wt-material-upload -b wt/material-upload
```

这样可以得到：

```text
bs-web/
bs-web-wt-xiaohuangche/
bs-web-wt-live-coupon/
bs-web-wt-material-upload/
```

它们可以同时打开在不同编辑器窗口里，但分支彼此独立。

## 反例

如果你真正想要的是三个目录都同时停在 `feat/batch-invite-remove-single-import`，那 `git worktree` 不合适。你需要的是：

```bash
git clone <repo-url> bs-web-a
git clone <repo-url> bs-web-b
git clone <repo-url> bs-web-c
```

然后每个目录再切到同一个分支。

## 可复用规则

`git worktree` 的主要目的，是在不重复完整 clone 仓库的前提下，让同一个项目并行处理多个分支和多个需求。  
如果你要的是“同一个分支在多个目录里同时存在”，那就用多个 clone，不要硬套 worktree。
