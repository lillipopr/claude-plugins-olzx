---
description: 调用限界上下文设计Skill，根据 PRD 生成限界上下文设计文档。支持两阶段工作流：先生成大纲版讨论优化，定稿后生成详细版。
calls-skill: spec-compiler:ddd-01-bounded-context
---

# /ddd-01-bc - 限界上下文设计命令

此命令调用 **ddd-01-bounded-context** Skill，从 PRD 生成限界上下文设计文档。

## 使用场景

- 已有 PRD 文档，需要生成限界上下文设计
- 需要进行业务能力分析
- 需要划分限界上下文
- 需要设计上下文映射关系

## 技术说明

**Command 类型**：直接调用 Skill（非 Agent）

**Skill 路径**：`{CLAUDE_PLUGIN_ROOT}/skills/ddd-01-bounded-context/SKILL.md`

**优势**：
- 更轻量：无需启动独立 Agent 进程
- 更快速：直接在当前会话中执行
- 更可控：Skill 包含完整流程指引，便于调试和优化
