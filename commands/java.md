---
name: java
description: 调用 Java 专家，实现后端代码/Review/Bugfix
---

# /java - Java 工程师命令

## 描述

调用 Java 后端专家，实现规格文档的后端部分，并负责代码审查和 Bug 修复。

## 使用方式

```bash
/java
```

## 场景选择

### 1. 实现后端代码

**前提条件**：已有规格文档

**输入**：规格文档路径

**执行流程**：
1. 调用 `java-expert` Agent
2. 分析规格文档中的后端部分
3. 遵循 Java DDD 分层架构：
   ```
   Controller → Application → Domain ← Gateway/Infra
                              ↑
                           Mapper
   ```
4. 生成各层代码：
   - Controller 层：接收请求、参数校验
   - Application 层：用例编排、事务管理
   - Domain 层：业务逻辑、不变量校验
   - Gateway/Infra 层：外部服务调用
   - Mapper 层：数据库访问
5. 确保代码质量：
   - 遵循 SOLID 原则
   - 遵循编码规范
   - 添加必要注释

**产出**：后端代码实现

### 2. Review 代码

**输入**：待审查的代码路径

**执行流程**：
1. 调用 `java-expert` Agent
2. 检查架构分层规范
3. 验证 SOLID 原则
4. 检查代码质量：
   - 命名规范
   - 异常处理
   - 并发安全
   - 性能考虑
5. 检查安全性：
   - SQL 注入防护
   - XSS 防护
   - CSRF 保护
6. 输出审查报告

**产出**：代码审查报告

### 3. 修复 Bug

**输入**：Bug 描述或测试失败信息

**执行流程**：
1. 调用 `java-expert` Agent
2. 分析 Bug 根本原因
3. 设计修复方案
4. 实现修复代码
5. 添加/更新测试用例
6. 验证修复

**产出**：修复后的代码 + 测试用例

## 架构分层

```
┌─────────────────────────────────────────────────────────────────┐
│                        Java DDD 分层架构                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Controller      │ 接收请求、参数校验、调用 Application           │
│  ─────────────────────────────────────────────────────────────  │
│  Application     │ 用例编排、事务管理、调用 Domain                │
│  ─────────────────────────────────────────────────────────────  │
│  Domain          │ 业务逻辑、不变量校验、领域事件                 │
│  ─────────────────────────────────────────────────────────────  │
│  Gateway/Infra   │ 外部服务调用、消息发送                         │
│  ─────────────────────────────────────────────────────────────  │
│  Mapper          │ 数据库 CRUD、ORM 映射                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 命名规范

| 层 | 类命名 | 示例 |
|----|--------|------|
| Controller | `XxxController` | `MembershipController` |
| Application | `XxxAppService` | `MembershipAppService` |
| Domain | `Xxx` (实体) / `XxxService` | `Membership` / `MembershipService` |
| Gateway | `XxxGateway` | `PaymentGateway` |
| Mapper | `XxxMapper` | `MembershipMapper` |

## 质量标准

| 检查项 | 标准 |
|--------|------|
| 架构分层 | 严格遵循 DDD 分层 |
| SOLID 原则 | 单一职责、开闭原则等 |
| 代码规范 | 遵循 Alibaba Java 规范 |
| 测试覆盖率 | 80%+ |
| 安全性 | 通过安全检查清单 |

## 相关文档

- [Java 专家 Skill](../skills/for-java-expert/SKILL.md)
- [Java DDD 分层规范](../rules/architecture/java-ddd-layers.md)
- [代码模板](../skills/for-java-expert/references/templates/)

## 示例

```
用户: /java

Claude: 请选择场景：
1. 实现后端代码
2. Review 代码
3. 修复 Bug

用户: 1

Claude: 请提供规格文档路径...

[调用 java-expert Agent，生成 DDD 分层代码]
```
