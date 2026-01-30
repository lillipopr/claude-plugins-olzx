---
name: ddd
description: 调用领域架构师，处理 DDD 设计的创建/修改/Review
---

# /ddd - 领域架构师命令

## 描述

调用资深领域架构师，处理 DDD 设计文档的创建、修改和审查。

## 使用方式

```bash
/ddd
```

## 场景选择

### 1. 创建 DDD 设计

**前提条件**：已有 PRD 文档

**输入**：PRD 文档路径

**执行流程**：
1. 调用 `domain-architect` Agent
2. 分析 PRD，识别领域概念
3. 设计领域模型：
   - 聚合根设计
   - 实体识别
   - 值对象定义
   - 领域服务
4. 设计限界上下文
5. 绘制上下文映射图

**产出**：《DDD 设计文档.md》

### 2. 修改 DDD 设计

**输入**：现有 DDD 文档、变更说明

**执行流程**：
1. 调用 `domain-architect` Agent
2. 分析变更对领域模型的影响
3. 更新聚合设计
4. 更新上下文映射
5. 标记变更版本

**产出**：更新后的 DDD 文档

### 3. Review DDD 设计

**输入**：待审查的 DDD 文档

**执行流程**：
1. 调用 `domain-architect` Agent
2. 检查领域模型设计
3. 验证聚合边界
4. 检查上下文映射合理性
5. 输出审查报告

**产出**：DDD 设计审查报告

## 质量闸口

| 检查项 | 标准 |
|--------|------|
| 聚合设计 | 聚合根清晰，边界合理 |
| 实体识别 | 实体有唯一标识和生命周期 |
| 限界上下文 | 上下文边界清晰，职责单一 |
| 上下文映射 | 映射关系明确，合作模式清晰 |
| 不变量 | 每个聚合的不变量明确 |

## 相关文档

- [领域架构师 Skill](../skills/for-domain-architect/SKILL.md)
- [DDD 方法论](../skills/for-domain-architect/references/methodology/ddd.md)
- [DDD 模板](../skills/for-domain-architect/references/templates/ddd-template.md)

## 示例

```
用户: /ddd

Claude: 请选择场景：
1. 创建 DDD 设计
2. 修改 DDD 设计
3. Review DDD 设计

用户: 1

Claude: 请提供 PRD 文档路径...

[调用 domain-architect Agent，创建 DDD 设计]
```
