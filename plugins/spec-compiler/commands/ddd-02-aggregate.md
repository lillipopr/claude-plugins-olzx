---
description: 调用聚合设计Skill，根据《限界上下文设计》文档生成《聚合设计》文档。
calls-skill: spec-compiler:ddd-02-aggregate
---

# /ddd-02-aggregate - 聚合设计命令

此命令调用 **ddd-02-aggregate** Skill，从《限界上下文设计》文档生成《聚合设计》文档。

## 技术说明

**Command 类型**：直接调用 Skill（非 Agent）

**Skill 路径**：`{CLAUDE_PLUGIN_ROOT}/skills/ddd-02-aggregate/SKILL.md`

**优势**：
- 更轻量：无需启动独立 Agent 进程
- 更快速：直接在当前会话中执行
- 更可控：Skill 包含完整流程指引，便于调试和优化
