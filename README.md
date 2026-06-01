# My Claude Settings

个人 Claude Code (CLI) 的全局配置文件，用于规范 AI 辅助编程的行为和流程。

## 文件说明

| 文件 | 用途 |
|------|------|
| `CLAUDE.md` | Claude Code 全局指令，包含行为规则、工具使用规范、项目上下文 |
| `memory/` | 持久化记忆文件，跨会话保留用户偏好和项目上下文 |

## 核心规则摘要

1. **多步骤任务必建 Todo** — 3+ 步骤或 2+ 文件的任务，先建 Todo 再动手
2. **完成前必须验证** — 声称完成前实际跑一遍确认
3. **先诊断再修改** — 遇到错误先定位根因，不硬猜
4. **知识时效性** — 不确定 API/版本时主动搜索
5. **不改无关代码** — 修 bug 就只修 bug，不顺手重构
6. **并行调用工具** — 独立操作放在同一条消息里发出

## 技术栈偏好

- 前端：React + Vite
- 后端：Python FastAPI
- AI：Claude API
- 数据库：PostgreSQL + pgvector
- 异步任务：Celery

## 文件来源

这些文件原本位于 `~/.claude/` 目录下，是 Claude Code 自动加载的配置。提取出来便于版本管理和备份。

> **注意：** `settings.json` 因包含 API 密钥，未纳入版本控制。可参考 `settings.example.json` 了解配置结构。
