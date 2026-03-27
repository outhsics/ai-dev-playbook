# AI Dev Playbook

AI 协作开发的长期经验库。  
A long-term knowledge base for AI-assisted software development.

## 仓库目标 | Purpose

把容易丢失在聊天记录、本地临时笔记、一次性项目上下文里的经验，沉淀成可搜索、可复用、可发布的长期资产。  
Turn lessons that would otherwise disappear into chat history, temporary local notes, or one-off project context into searchable, reusable, publishable assets.

## 结构 | Structure

- `AGENTS.md`: 给任意 AI 的工作说明 | instructions for any AI working in this repo
- `docs/`: 正式经验文章 | finished notes and practical write-ups
- `docs/_meta/`: 稳定上下文与发布流程 | stable context and publishing workflow
- `templates/`: 可复用模板 | reusable templates

## 任意 AI 的使用方式 | Use With Any AI

让 AI 先读这三个文件：  
Ask the AI to read these files first:

1. `AGENTS.md`
2. `docs/_meta/user-context.md`
3. `docs/_meta/publishing-workflow.md`

## 默认写作标准 | Default Writing Standard

- 默认支持中英文，除非用户明确要求单语
- 内容优先简洁、实用、可检索
- 每篇尽量聚焦一个问题和一个可复用解法
- 正式长文优先拆成中文稿和英文稿

- Support both Chinese and English unless the user explicitly asks for one language only
- Optimize for concise, practical, searchable writing
- Keep each note focused on one problem and one reusable solution
- Prefer separate Chinese and English files for public long-form articles

## 推荐流程 | Recommended Workflow

1. 问题解决后，立刻提炼成一条经验
2. 写出一个真实例子和一个适用边界
3. 保存到 `docs/`
4. 需要发布时直接提交并推送

1. Once a problem is solved, turn it into a note immediately
2. Add one real example and one boundary
3. Save it under `docs/`
4. Commit and push when publishing is wanted

## 当前文章 | Current Notes

- [Local AI Workspace Best Practices](./docs/local-ai-workspace.md)
- [Git Worktree vs Clone (中文)](./docs/workflow/git-worktree-vs-clone.zh-CN.md)
- [Git Worktree vs Clone (English)](./docs/workflow/git-worktree-vs-clone.en.md)
