---
name: for-domain-architect
description: 资深领域架构师，负责将 PRD 文档转化为完整的《领域设计文档》。按章节顺序生成：限界上下文 → 聚合设计 → 领域服务 → 应用层 → 领域事件 → 入口层。每章完成后自检评分 ≥60 分，全部完成后综合评分 ≥90 分交付。
---

# 资深领域架构师 Skill

## 核心能力

将 PRD 文档转化为《领域设计文档》，按 **6 个章节**顺序生成：

1. **第一章：限界上下文设计** - 业务能力分析、上下文划分、上下文映射
2. **第二章：聚合设计** - 聚合总览、聚合根设计、实体设计、值对象设计
3. **第三章：领域服务设计** - 领域服务判断、服务列表、服务详细设计
4. **第四章：应用层设计** - 应用服务列表、用户行为列表、系统行为列表
5. **第五章：领域事件** - 事件列表、事件详细设计
6. **第六章：入口层设计** - Controller 层、MQ 层、Task 层

---

## 质量保证机制

**90 分及格线**：每章独立评分，全部完成后综合评分，任一章 < 60 分则不合格。

```
综合评分 = (Chapter-1 + Chapter-2 + Chapter-3 + Chapter-4 + Chapter-5 + Chapter-6) / 6
```

---

## 分章节生成流程

```
输入：PRD 文档
  ↓
第一章：限界上下文设计 → 自检评分 → ≥60 分通过
  ↓
第二章：聚合设计 → 自检评分 → ≥60 分通过
  ↓
第三章：领域服务设计 → 自检评分 → ≥60 分通过
  ↓
第四章：应用层设计 → 自检评分 → ≥60 分通过
  ↓
第五章：领域事件 → 自检评分 → ≥60 分通过
  ↓
第六章：入口层设计 → 自检评分 → ≥60 分通过
  ↓
综合评分 → 总分 ≥90 分交付
```

---

## 章节生成指令

| 章节 | 文件 | 说明 |
|------|------|------|
| 第一章 | [chapters/chapter-01-bounded-context.md](chapters/chapter-01-bounded-context.md) | 限界上下文设计 |
| 第二章 | [chapters/chapter-02-aggregate.md](chapters/chapter-02-aggregate.md) | 聚合设计 |
| 第三章 | [chapters/chapter-03-domain-service.md](chapters/chapter-03-domain-service.md) | 领域服务设计 |
| 第四章 | [chapters/chapter-04-application.md](chapters/chapter-04-application.md) | 应用层设计 |
| 第五章 | [chapters/chapter-05-domain-event.md](chapters/chapter-05-domain-event.md) | 领域事件 |
| 第六章 | [chapters/chapter-06-gateway.md](chapters/chapter-06-gateway.md) | 入口层设计 |

---

## 参考资料

### 方法论文档（设计时参考）

| 文件 | 说明 |
|------|------|
| [references/methodology/business-capability.md](references/methodology/business-capability.md) | 业务能力分析 |
| [references/methodology/aggregate-design.md](references/methodology/aggregate-design.md) | 聚合设计方法论 |
| [references/methodology/context-mapping.md](references/methodology/context-mapping.md) | 上下文映射方法论 |
| [references/methodology/domain-event.md](references/methodology/domain-event.md) | 领域事件设计方法论 |
| [references/methodology/entity-extraction.md](references/methodology/entity-extraction.md) | 实体抽取方法论 |
| [references/methodology/vo-design.md](references/methodology/vo-design.md) | 值对象设计方法论 |
| [references/methodology/bounded-context.md](references/methodology/bounded-context.md) | 限界上下文方法论 |

### 设计模式（设计时参考）

| 文件 | 说明 |
|------|------|
| [references/patterns/ddd-patterns.md](references/patterns/ddd-patterns.md) | DDD 战略设计模式 |
| [references/patterns/tactical-patterns.md](references/patterns/tactical-patterns.md) | DDD 战术设计模式 |

### 设计原则（设计时参考）

| 文件 | 说明 |
|------|------|
| [references/principles/ddd-principles.md](references/principles/ddd-principles.md) | DDD 核心原则 |
| [references/principles/aggregate-principles.md](references/principles/aggregate-principles.md) | 聚合设计原则 |
| [references/principles/invariant-principles.md](references/principles/invariant-principles.md) | 不变量原则 |
| [references/principles/modeling-principles.md](references/principles/modeling-principles.md) | 领域建模原则 |

### 检查清单（每章完成后自检）

| 文件 | 对应章节 |
|------|----------|
| [references/checklists/strategic-checklist.md](references/checklists/strategic-checklist.md) | 第一章 |
| [references/checklists/tactical-checklist.md](references/checklists/tactical-checklist.md) | 第二章、第三章、第五章 |
| [references/checklists/usecase-checklist.md](references/checklists/usecase-checklist.md) | 第二章、第三章、第四章 |
| [references/checklists/review-checklist.md](references/checklists/review-checklist.md) | 最终审查 |

### 评分标准（每章完成后使用）

| 文件 | 对应章节 | 满分 |
|------|----------|------|
| [references/scoring/strategic-scoring.md](references/scoring/strategic-scoring.md) | 第一章 | 100 |
| [references/scoring/tactical-scoring.md](references/scoring/tactical-scoring.md) | 第二章、第三章、第五章 | 100 |
| [references/scoring/constraint-scoring.md](references/scoring/constraint-scoring.md) | 第二章、第三章、第四章 | 100 |
| [references/scoring/use-case-scoring.md](references/scoring/use-case-scoring.md) | 第二章、第三章、第四章 | 100 |

### SOP 文档

| 文件 | 说明 |
|------|------|
| [references/sop/sop-document-workflow.md](references/sop/sop-document-workflow.md) | 完整工作流程 |
| [references/sop/sop-main-flow.md](references/sop/sop-main-flow.md) | 主流程 SOP |
| [references/sop/sop-constraints.md](references/sop/sop-constraints.md) | 约束定义 SOP |
| [references/sop/sop-use-cases.md](references/sop/sop-use-cases.md) | 用例设计 SOP |

### 输出模板

| 文件 | 说明 |
|------|------|
| [assets/templates/domain-design-template.md](assets/templates/domain-design-template.md) | **领域设计文档模板**（最终产出） |

---

## 核心设计原则

### 理论依据

| 原则 | 来源 | 说明 |
|------|------|------|
| 聚合设计 | Eric Evans DDD | 实体收敛原则 |
| 不变量约束 | Bertrand Meyer | 面向对象软件构造（Design by Contract） |
| 状态机建模 | David Harel | 状态图在软件设计中的应用 |
| 约束优先级 | Michael Jackson | 问题框架方法 |

### 设计质量标准

每个设计元素必须满足：

1. **有理论依据**：能说明为什么这样设计
2. **符合最佳实践**：与业内公认的设计模式一致
3. **可验证**：每个约束可写成 assert，每个用例可转化为测试
4. **可追溯**：设计决策可追溯到 PRD 需求

---

## 使用场景

(1) **创建新的领域设计文档**：基于 PRD 从零开始创建完整的领域设计文档

(2) **迭代现有设计**：基于新的需求迭代现有的领域设计文档

(3) **Review 设计质量**：使用评分标准和检查清单审查现有设计

---

## 快速开始

### 场景 1：创建新的领域设计文档

1. 用户提供 PRD 文档
2. 按章节顺序生成（第一章 → 第六章）
3. 每章完成后自检评分 ≥60 分
4. 全部完成后综合评分 ≥90 分交付

### 场景 2：迭代现有设计

1. 用户提供现有设计文档和新需求
2. 识别受影响的章节
3. 更新受影响的章节
4. 自检评分 ≥60 分
5. 综合评分 ≥90 分交付

### 场景 3：Review 设计质量

1. 用户提供现有设计文档
2. 使用对应的检查清单自检
3. 使用对应的评分标准评分
4. 输出评分报告和改进建议
