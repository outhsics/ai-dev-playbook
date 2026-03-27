# 多 AI 并行开发时的分支和目录规则

英文版见：[multi-ai-branch-and-directory-rules.en.md](./multi-ai-branch-and-directory-rules.en.md)
配套文章见：[git-worktree-vs-clone.zh-CN.md](./git-worktree-vs-clone.zh-CN.md)

## 问题

当一个项目开始同时处理多个需求，并且希望把不同任务交给不同 AI 时，真正容易失控的不是代码本身，而是目录和分支没有规则。

常见混乱包括：

- 多个 AI 同时在同一个目录里改文件
- 不同需求共用一个分支
- 编辑器开了很多窗口，但其实都在指向同一套工作区
- 需求资料、临时说明、提交记录混在一起

## 背景

很多团队在引入 AI 后，第一步只解决了“能不能让 AI 写代码”，但没有解决“多个 AI 怎么安全地同时工作”。

如果没有明确规则，多 AI 并行开发通常会带来这些问题：

- 改动互相覆盖
- 上下文串线
- 提交历史难看
- 合并时不知道谁改了什么
- AI 在错误目录里继续工作

所以真正需要的不是“再开几个窗口”，而是一套简单、稳定、能重复执行的分支和目录约定。

## 有效解法

最实用的规则是：

1. 一个需求一个目录
2. 一个需求一个分支
3. 一个目录只给一个 AI
4. 一个目录只开一个主要编辑器窗口

如果项目本身已经在 Git 管理下，那么目录层一般优先用 `git worktree` 来做隔离。

## 推荐目录规则

主仓库目录只保留主线或主功能分支。  
并行需求使用兄弟目录，统一命名。

例如：

```text
bs-web/
bs-web-wt-xiaohuangche/
bs-web-wt-live-coupon/
bs-web-wt-material-upload/
```

推荐约定：

- 主目录只处理主线任务
- 并行目录统一使用 `*-wt-*` 命名
- 目录名直接体现需求名，避免抽象编号

## 推荐分支规则

分支不要继续堆在一个通用名字上，例如所有工作都往同一个 `feat/xxx` 分支里塞。

更好的规则是：

- 主功能线一个主分支
- 每个并行需求从主功能线拆子分支

例如：

```text
feat/batch-invite-remove-single-import
wt/xiaohuangche
wt/live-coupon
wt/material-upload
```

如果你希望命名更直观，也可以写成：

```text
feat/batch-invite/xiaohuangche
feat/batch-invite/live-coupon
feat/batch-invite/material-upload
```

重点不是前缀本身，而是每个并行需求必须有独立分支。

## AI 操作规则

对 AI 来说，最重要的不是“写得多快”，而是不要跑错目录。

建议给每个 AI 固定这几条规则：

1. 开始前先确认当前目录
2. 开始前先确认当前分支
3. 只处理当前 worktree 对应的需求
4. 不要顺手修改另一个并行需求的文件
5. 本地需求资料只放当前目录下的 `.ai-local/`

例如：

```text
.ai-local/xiaohuangche/
.ai-local/live-coupon/
```

## 提交规则

并行开发时，提交粒度比平时更重要。

建议：

- 一个需求只提交自己的改动
- 不要把多个需求混进同一个 commit
- commit message 直接体现需求目的
- 完成后先回到对应分支审查，再合并

## 不推荐的做法

以下做法在多 AI 场景里风险很高：

- 多个 AI 共享同一目录
- 多个 AI 共享同一分支
- 在一个目录里顺手处理多个需求
- 让 AI 在不确认路径和分支的情况下直接开工

这些做法短期看起来省事，长期几乎一定会把上下文、提交历史和责任边界全部打乱。

## 最小示例

```bash
git worktree add ../bs-web-wt-xiaohuangche -b wt/xiaohuangche
git worktree add ../bs-web-wt-live-coupon -b wt/live-coupon
git worktree add ../bs-web-wt-material-upload -b wt/material-upload
```

然后：

- 一个窗口打开 `bs-web-wt-xiaohuangche`
- 一个窗口打开 `bs-web-wt-live-coupon`
- 一个窗口打开 `bs-web-wt-material-upload`
- 每个窗口只交给一个 AI

## 可复用规则

多 AI 并行开发时，先管理目录和分支，再管理代码。  
最稳的默认规则就是：一个需求一个目录，一个需求一个分支，一个目录只给一个 AI。
