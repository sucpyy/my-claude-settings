# CLAUDE.md

---

## 默认行为规则（每次对话自动生效）

### 1. 多步骤任务必须用 TodoWrite

任何涉及 3+ 步骤或 2+ 文件的任务，**必须先建 Todo 再动手**。只有单文件单步骤的小修改可以跳过。

- 开始一项任务 → 标记 `in_progress`
- 完成一项 → 立刻标记 `completed`，不要批量完成
- 同一时间只有一项 `in_progress`

### 2. 声称完成前必须验证

说"完成""修好了""通过了"之前，实际跑一遍验证：

- 改了代码 → 跑 lint / 类型检查 / 相关测试
- 写了新功能 → 跑一遍确认能用
- 修了 bug → 确认 bug 不再复现
- 文件操作 → 确认文件存在、内容正确

**不允许验证通过后再继续改其他东西然后说"做好了"——验证是最后一步。**

### 3. 遇到错误先诊断，别急着改

- 出现一次错误 → 读错误信息，定位根因
- 同一个操作连续失败 3 次 → 停下来，换思路，不要继续重试同样的方法
- 不确定原因时 → 用 `mcp__ccd_session__spawn_task` 记录下来，而不是硬猜

### 4. 知识时效性

训练数据截止 2025 年初。遇到以下情况**必须搜索**：

- 框架/库的主版本号不确定
- API 可能有 breaking change
- 配置项可能已废弃或改名
- 任何"我记得好像是..."的情况

搜索时用当前年份。

### 5. 工具使用规范

- **Bash** 优先用专用工具：Read 替代 cat/head/tail，Glob 替代 find/ls，Grep 替代 grep/rg，Write/Edit 替代 echo/heredoc
- **Edit** 优先于 Write（修改已有文件用 Edit，只有新建文件才用 Write）
- **并行**：多个独立的 Read/Bash/Glob/Grep 调用放在同一条消息里发，不要串行等待
- **不改无关代码**：修 bug 就只修 bug，不要顺手重构不相关的部分

### 6. 代码质量

- 写完代码后对比原有代码风格，保持一致性
- 函数/变量命名清晰，缩写只在众所周知的范围内用
- 复杂逻辑加注释说"为什么"，不是"做了什么"
- 新增代码有对应测试覆盖

### 7. 项目上下文

每个项目的关键决策和当前状态，记录在对应项目的 CLAUDE.md 或 Obsidian 笔记中。新会话开始时，我会主动读取相关上下文。

---

## 可用技能（Skills）

根据任务类型，**主动建议**用户使用对应技能。

### Superpowers 开发流程（自动触发）
- `/brainstorming` — 任何创造性工作前必须先过头脑风暴
- `/writing-plans` — 有规格后先写实现计划
- `/executing-plans` — 按计划执行，带审查检查点
- `/subagent-driven-development` — 用子 Agent 并行执行独立任务
- `/test-driven-development` — 实现前先写测试
- `/verification-before-completion` — 声称完成前先跑验证
- `/dispatching-parallel-agents` — 多个独立任务并行派发
- `/requesting-code-review` — 完成任务后请求代码审查
- `/receiving-code-review` — 收到审查反馈后的处理流程
- `/systematic-debugging` — 遇到 bug 先结构化调试，别急着改
- `/finishing-a-development-branch` — 分支完成后整合流程
- `/using-git-worktrees` — 创建隔离的 git worktree 环境
- `/using-superpowers` — Superpowers 使用指南
- `/writing-skills` — 创建/编辑 Skill 的最佳实践

### 规划 & 设计
- `/to-prd` — 对话内容 → PRD + GitHub Issue
- `/to-issues` — 计划/规格 → 独立 Issues
- `/grill-me` — 对方案进行「拷问式」审查
- `/design-an-interface` — 并行生成多种接口设计方案
- `/request-refactor-plan` — 创建详细重构计划
- `/domain-model` — 领域建模
- `/zoom-out` — 从更高视角审视当前工作

### 开发
- `/tdd` — 测试驱动开发（红-绿-重构循环）
- `/triage-issue` — 定位 bug 根因 + 修复计划
- `/improve-codebase-architecture` — 代码架构分析改进
- `/scaffold-exercises` — 创建练习目录结构
- `/qa` — 质量保证

### 前端设计
- `/frontend-design` — 创建有辨识度、生产级的前端界面

### 工具 & 配置
- `/git-guardrails-claude-code` — 拦截危险 git 命令
- `/setup-pre-commit` — 配置 pre-commit hooks
- `/update-config` — 修改 settings.json / 权限 / 环境变量 / hooks

### 写作 & 知识
- `/write-a-skill` — 创建新技能
- `/edit-article` — 编辑优化文章
- `/ubiquitous-language` — 提取通用语言词汇表
- `/obsidian-vault` — 管理 Obsidian 笔记

### 行为规范
- `/karpathy-guidelines` — Andrej Karpathy 的编码行为准则
- `/caveman` — 极简沟通模式，省 75% token
