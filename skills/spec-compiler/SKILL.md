---
name: spec-compiler
description: |
  规格编译器：将模糊需求编译为确定性规格文档，实现"人管变化，AI 写实现"。

  核心理念：文档是"新时代的代码"，AI IDE 是"编译器"。

  完整编排流程：
  - Stage 1: PRD（PM 产出产品需求文档）
  - Stage 2: DDD Design（架构师产出领域设计）
  - Stage 3: Spec Modeling（规格建模：实体/状态/不变量/用例）
  - Stage 4: Artifact Derivation（工件推导：分层架构/接口契约/实现）
  - Stage 5: Test Generation（测试生成：从用例推导测试代码，TDD 集成）

  支持场景：
  - 首次功能建设（完整流程）
  - 功能迭代（增量更新）
  - Bug 修复（用例补充 → 工件修复）
  - 功能下线（逆向清理）

  支持架构：
  - 后端 DDD 分层（Controller → Application → Domain → Gateway/Infra → Mapper）
  - 移动端 MVVM 分层（View → ViewModel → Service → Gateway → Network）
  - Vue 3 前端分层（View → Composable → Service → API → Request）
---

# 规格编译器（Spec Compiler）

## 核心理念

**人管变化，AI 写实现**

```
传统模式：需求 → 人写代码 → 测试 → 交付
新范式：  需求 → 人写文档 → AI 编译代码 → 测试 → 交付
```

- 人负责：需求定义、领域设计、规格审核、验收
- AI 负责：规格建模、工件推导、代码生成、测试实现
- 代码是可替换工件，规格 + 用例才是资产

## 完整编排流程

```
┌─────────────────────────────────────────────────────────────────┐
│                         完整功能建设流程                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Stage 1: PRD                                                   │
│  ├─ 执行者: PM                                                   │
│  ├─ 产出: 《产品需求文档》                                         │
│  ├─ 详见: stages/01-prd.md                                       │
│  └─ 闸口: 需求清晰、边界明确、验收标准可测                           │
│           ↓                                                     │
│  Stage 2: DDD Design                                            │
│  ├─ 执行者: 架构师                                                │
│  ├─ 产出: 《DDD 设计文档》                                         │
│  ├─ 详见: stages/02-ddd-design.md                                │
│  └─ 闸口: 领域边界清晰、聚合设计合理、上下文映射完整                  │
│           ↓                                                     │
│  Stage 3: Spec Modeling                                         │
│  ├─ 执行者: AI + 人工审核                                         │
│  ├─ 产出: 《规格建模文档》                                         │
│  ├─ 详见: stages/03-spec-modeling.md                             │
│  └─ 闸口: 状态完备、不变量完整、用例覆盖（含 Bad Case）              │
│           ↓                                                     │
│  Stage 4: Artifact Derivation                                   │
│  ├─ 执行者: AI + 人工审核                                         │
│  ├─ 产出: 《工件推导文档》                                         │
│  ├─ 详见: stages/04-artifact-derivation.md                       │
│  └─ 闸口: 分层清晰、契约一致、可直接编码                            │
│           ↓                                                     │
│  Stage 5: Test Generation                                       │
│  ├─ 执行者: AI + 人工审核                                         │
│  ├─ 产出: 《测试代码》                                            │
│  ├─ 详见: stages/05-test-generation.md                           │
│  └─ 闸口: 测试覆盖所有用例、TDD RED 阶段就绪                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 场景路由

| 场景 | 命令 | 执行阶段 | 说明 |
|------|------|---------|------|
| **首次功能建设** | `/spec-new` | 1 → 2 → 3 → 4 | 完整流程 |
| **功能迭代** | `/spec-iter` | 2 → 3 → 4 | 基于已有 PRD 增量更新 |
| **Bug 修复** | `/spec-fix` | 3 → 4 | 定位问题 → 补充用例 → 推导修复 |
| **功能下线** | `/spec-offline` | 3 → 4（逆向） | 删除用例 → 删除工件 → 清理代码 |

详见 `workflows/` 目录下的场景工作流。

## 核心原则

详见 `rules/core-principles.md`，关键闸口：

| 闸口 | 检查点 | 不通过则 |
|------|--------|----------|
| **PRD 闸** | 需求清晰、边界明确 | 不进入 DDD 设计 |
| **DDD 闸** | 领域边界清晰、聚合合理 | 不进入规格建模 |
| **建模闸** | 状态完备、不变量完整、用例覆盖 | 不进入工件推导 |
| **工件闸** | 分层清晰、契约一致 | 不允许生成代码 |
| **熵控闸** | 功能下线时删 case + 删代码 | 不允许遗留死代码 |

## 架构识别

使用此 skill 时，首先识别项目架构类型：

| 检测项 | 后端 DDD | iOS (SwiftUI) | Android | Vue 3 |
|--------|---------|--------------|---------|--------|
| pom.xml / build.gradle | ✅ | - | - | - |
| *.swift / @StateObject | - | ✅ | - | - |
| *.kt / ViewModel | - | - | ✅ | - |
| package.json + vue | - | - | - | ✅ |

架构规范详见 `~/.claude/rules/architecture/`。

## 快速导航

### 按阶段
- [Stage 1: PRD](stages/01-prd.md)
- [Stage 2: DDD Design](stages/02-ddd-design.md)
- [Stage 3: Spec Modeling](stages/03-spec-modeling.md)
- [Stage 4: Artifact Derivation](stages/04-artifact-derivation.md)

### 按场景
- [首次功能建设](workflows/full-feature.md)
- [功能迭代](workflows/feature-iteration.md)
- [Bug 修复](workflows/bug-fix.md)
- [功能下线](workflows/feature-deprecation.md)

### 方法论
- [实体抽取 DDD 原则](methodology/entity-extraction.md)
- [状态空间设计](methodology/state-space-design.md)
- [不变量定义](methodology/invariants.md)
- [意图 vs 事实](methodology/intent-vs-fact.md)

### 模板
- [PRD 模板](templates/tpl-prd.md)
- [DDD 设计模板](templates/tpl-ddd-design.md)
- [规格建模模板](templates/tpl-spec-modeling.md)
- [工件推导模板](templates/tpl-artifact-derivation.md)

## AI 执行流程

### 场景识别

当用户提出需求时：

1. **识别场景** → 首次建设 / 迭代 / Bug 修复 / 下线
2. **识别架构** → 后端 / iOS / Android / 前端
3. **路由到对应工作流** → 调用相应 Agent 执行

### 闸口控制

**每个 Stage 完成后必须等待用户确认**：

```
Stage N 完成 → 输出产出物 → 提醒用户 Review → 等待确认 → 进入 Stage N+1
```

**禁止行为**：
- 不能在用户未确认时自动进入下一 Stage
- 不能跳过 Review 闸口
- 不能假设用户已同意而继续执行

**必须行为**：
- 每个 Stage 完成后明确提醒用户 Review
- 清晰列出 Review 要点
- 等待用户明确的正面确认
- 修改后再次提醒 Review

## 快速开始示例

**输入**：用户订阅会员，每天刷新 100 点券

**Stage 1 PRD**：
- 功能描述、用户故事、验收标准

**Stage 2 DDD**：
- 聚合根：Membership
- 实体：CouponGrant
- 限界上下文：会员上下文、点券上下文

**Stage 3 Spec Modeling**：
- 状态：M0(非会员) → M1(生效中) → M2(已过期)
- 不变量：INV-1 只有 M1 才能发放点券
- 用例：覆盖所有状态转移 + Bad Case

**Stage 4 Artifact Derivation**：
- 后端：Controller/Application/Domain/Gateway 分层
- 接口契约：API 定义、DTO、错误码
- 实现位置映射
