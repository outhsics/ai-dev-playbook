# AGENTS.md

## 仓库定位 | Repository Role

这是一个给 Terre 使用的长期知识库，用来沉淀 AI 协作开发中的实战经验。  
This is a long-term repository for Terre to preserve practical lessons from AI-assisted development.

## 首先阅读 | Read First

开始改动前先读：

1. `docs/_meta/user-context.md`
2. `docs/_meta/publishing-workflow.md`

Before making changes, read:

1. `docs/_meta/user-context.md`
2. `docs/_meta/publishing-workflow.md`

## 主要任务 | Primary Task

当用户说某个问题已经解决、值得记录、想整理成文章、想发布时，你应当默认把它转成结构化的长期笔记，而不是停留在聊天总结。  
When the user says a problem has been solved, should be remembered, turned into an article, or published, default to turning it into a durable structured note instead of leaving it as chat-only output.

## 默认产出标准 | Default Output Standard

- 默认支持中英文，除非用户明确要求单语
- 标题优先可搜索，不要追求花哨
- 每篇聚焦一个问题或一个工作流
- 至少保留一个真实例子
- 明确说明何时不适用
- 可读、可复用、可检索

- Support both Chinese and English by default unless the user explicitly asks for one language only
- Prefer searchable titles over clever titles
- Keep each note focused on one problem or workflow
- Include at least one real example
- State when the pattern should not be used
- Optimize for readability, reuse, and searchability

## 语言策略 | Language Strategy

- 仓库级规则、模板、流程文档可以中英同页
- 面向公开阅读的正式文章，优先拆成中文和英文两个完整文件
- 不推荐在正式长文里逐段中英混排，阅读体验通常更差

- Repository-level rules, templates, and workflow docs may stay bilingual in one file
- Public-facing articles should usually be split into one full Chinese file and one full English file
- Avoid paragraph-by-paragraph mixed-language long-form articles unless there is a strong reason

## 推荐动作 | Preferred Actions

在可行时直接做完：

1. 提炼可复用经验
2. 在 `docs/` 中创建或更新文章
3. 优化标题和文件名
4. 用文档类提交信息提交
5. 用户明确要发布时直接推送

When feasible, complete the work end to end:

1. Distill the reusable lesson
2. Create or update a note under `docs/`
3. Improve the title and filename
4. Commit with a docs-focused message
5. Push when the user clearly wants publishing

## 文件落点 | File Placement

- `docs/`: 正式保留的文章 | finished notes worth keeping
- `docs/_meta/`: 稳定规则、上下文、流程 | stable rules, context, workflows
- `templates/`: 以后复用的模板 | templates for future notes

## 什么时候再问用户 | When To Ask

只有在会明显影响发布结果时再问，例如：

- 公开还是私有
- 只写中文、只写英文，还是保持双语
- 要发成粗稿，还是先打磨

Only ask when the choice materially changes what gets published, such as:

- public vs private
- Chinese only, English only, or bilingual
- publish a rough note vs polish first
