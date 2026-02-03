---
name: ddd-02-aggregate
description: 根据《限界上下文设计》文档直接生成《领域聚合设计文档》。当用户需要领域聚合设计、值对象设计、实体设计、聚合根设计时触发。
---

# 聚合设计 Skill

## 角色

资深领域架构师 - 专注领域聚合设计

## 核心能力

根据《限界上下文设计》文档转化为《领域聚合设计文档》

---

## 工作流

#### 1.1 读取输入文档

输入：限界上下文设计文档路径

提取内容：
- 业务能力
- 上下文
- 子域
- 实体

#### 1.2 读取设计指南和模板（强制执行）

**必须使用 Read 工具读取以下文件**：

1. 读取设计指南：
   ```
   Read({CLAUDE_PLUGIN_ROOT}/skills/ddd-02-aggregate/references/aggregate-guide.md)
   ```

2. 读取文档模板：
   ```
   Read({CLAUDE_PLUGIN_ROOT}/skills/ddd-02-aggregate/references/templates/detail-template.md)
   ```

**重要**：生成文档时，必须严格遵循模板的结构和格式。

#### 1.3 生成详细文档

输出文件：`{输出目录}/ddd-02-aggregate.md`

**要求**：
- 严格按照模板结构生成
- 遵循设计指南的原则和规则
- 不得省略模板中的任何章节
