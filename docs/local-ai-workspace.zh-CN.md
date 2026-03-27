# 本地 AI 工作区最佳实践

英文版见：[local-ai-workspace.en.md](./local-ai-workspace.en.md)

## 问题

使用 AI 辅助开发时，需求截图、PRD、调研材料、草稿和工具配置经常只适合留在本地。它们对开发有帮助，但不应该污染共享仓库，也不应该被误推到 GitHub。

## 常见坏做法

- 每个项目都临时改一次 `.gitignore`
- 本地 AI 工具目录长期出现在 `git status`
- 需求资料散落在临时目录，没有统一约定
- 对未跟踪资料目录使用 `assume-unchanged` 或 `skip-worktree`

## 推荐方案

分两层处理：

1. 跨项目通用的本地资料，走全局忽略
2. 某个仓库专属的 AI 工具配置，走仓库本地忽略

## 全局忽略

先配置全局 Git ignore 文件：

```bash
git config --global core.excludesFile ~/.gitignore_global
```

统一约定一个本地资料目录：

```gitignore
.ai-local/
```

然后所有仓库都能这样放：

```text
.ai-local/xiaohuangche/
.ai-local/new-feature/
.ai-local/research/
```

好处：

- 所有仓库通用
- 不用反复改项目 `.gitignore`
- 更容易告诉 AI 去哪里读资料

## 仓库本地忽略

对只在当前仓库有意义的工具配置，用 `.git/info/exclude`。

示例：

```gitignore
.claude/
```

这样不会把团队级忽略规则带进仓库历史。

## 实用判断规则

- `.ai-local/` 放本地需求资料、截图、提示词、草稿
- `.git/info/exclude` 放仓库专属 AI 工具目录
- 团队共享的正式文档仍然应该正常跟踪

## 不适用场景

不要把团队必须评审、维护或依赖的文件藏进本地目录。

## 最小示例

```text
my-project/
  .ai-local/
    xiaohuangche/
    feature-b-brief/
  .claude/
  src/
  package.json
```

## 总结

如果 AI 需要读这些资料，但 Git 不该跟踪它们，就给这些资料一个稳定的本地位置。对大多数项目来说，`.ai-local/` 加上有选择地使用 `.git/info/exclude` 就足够了。
