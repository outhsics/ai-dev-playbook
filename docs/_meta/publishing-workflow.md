# Publishing Workflow | 发布流程

## 目标 | Goal

把一次真实解决的问题，快速转成长期可复用、可公开的知识。  
Turn a real solved problem into durable, reusable, publishable knowledge quickly.

## 默认流程 | Default Workflow

1. 写清楚真实问题
2. 去掉聊天上下文里的噪音
3. 提炼可复用规则
4. 补一个真实例子
5. 说明边界或反模式
6. 存到 `docs/`
7. 提交
8. 推送

1. Capture the real problem
2. Remove chat-specific noise
3. Extract the reusable rule
4. Add one real example
5. State a boundary or anti-pattern
6. Save it under `docs/`
7. Commit
8. Push

## 命名规则 | Naming Rules

- 文件名要可搜索
- 优先按主题命名，不要只按日期命名
- 标题优先表达问题和解法

- Use searchable filenames
- Prefer topic-based names over date-only names
- Let titles clearly express the problem and the solution

示例 | Examples:

- `local-ai-workspace.md`
- `git-hygiene-for-ai-projects.md`
- `handoff-context-between-ai-tools.md`

## 推荐结构 | Recommended Shape

1. Problem | 问题
2. Context | 背景
3. Working Solution | 有效解法
4. Example | 例子
5. Boundaries | 边界
6. Reusable Rule | 可复用规则

## 发布阈值 | Publish Threshold

只要具备下面三点，就值得发布：

- 一个真实问题
- 一个已经验证可用的解法
- 一个能让读者立刻理解的例子

Publish once you have these three things:

- one real problem
- one solution that actually worked
- one example that makes it concrete

## 新建还是更新 | New File Or Update

如果这条经验本身能独立成立，就新建文件。  
如果它只是已有文章的补充案例、细化规则或更好的例子，就更新原文。  

Create a new file when the lesson stands on its own.  
Update an existing note when it is clearly a refinement, subcase, or better example of the same practice.
