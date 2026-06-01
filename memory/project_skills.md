---
name: 技能主动提醒
description: 用户安装了20+技能但怕忘记使用，需要主动提醒
type: project
originSessionId: 5cb30dc6-8151-42ca-aae1-ba589e91e44a
---
用户在 `~/.claude/skills/` 安装了 22 个技能（来自 mattpocock/skills 和 andrej-karpathy-skills）。

**规则：** 涉及以下场景时，主动询问用户是否使用对应技能：
- 需要写方案/规划时 → `/to-prd`、`/grill-me`
- 需要拆分任务时 → `/to-issues`
- 需要设计接口/模块时 → `/design-an-interface`
- 写测试/修 bug → `/tdd`、`/triage-issue`
- 需要重构 → `/request-refactor-plan`、`/improve-codebase-architecture`
- 需要配置 git 安全 → `/git-guardrails-claude-code`
- 需要写文档/文章 → `/edit-article`
- 需要严谨编码 → `/karpathy-guidelines`
