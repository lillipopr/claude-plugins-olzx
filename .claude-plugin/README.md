# Spec Compiler Kit 插件开发指南

## 概述

Spec Compiler Kit 是一个专业化的 Claude Code 插件，实现"人管变化，AI 写实现"的确定性软件开发范式。

## 目录结构

```
spec-compiler-kit/
├── .claude-plugin/
│   ├── plugin.json           # 插件核心配置
│   ├── marketplace.json       # Marketplace 配置
│   ├── hooks/                 # Hooks 脚本
│   ├── scripts/               # 安装/卸载脚本
│   ├── README.md             # 本文档
│   ├── HOOKS.md              # Hooks 开发规范
│   ├── VERSIONING.md         # 版本管理规范
│   └── PUBLISHING.md         # 发布流程指南
├── agents/                    # Agent 定义
│   ├── planner.md
│   ├── domain-architect.md
│   ├── product-manager.md
│   ├── spec-compiler-v4.md
│   ├── java-expert.md
│   ├── ios-expert.md
│   ├── frontend-expert.md
│   └── tdd-expert.md
├── commands/                  # Command 定义
│   ├── dev.md
│   ├── dev-feature.md
│   ├── dev-review.md
│   ├── dev-test.md
│   ├── dev-pr.md
│   ├── dev-refactor.md
│   ├── dev-fix.md
│   ├── dev-security.md
│   └── test.md
├── skills/                    # Skills 知识库
│   ├── for-spec-compiler-v4/
│   ├── for-domain-architect/
│   ├── for-product-manager/
│   ├── for-java-expert/
│   ├── for-ios-expert/
│   ├── for-frontend-expert/
│   └── for-tdd-expert/
├── rules/                     # 规则定义
│   ├── agents.md
│   ├── architecture/
│   │   ├── java-ddd-layers.md
│   │   ├── ios-mvvm-layers.md
│   │   └── vue3-layers.md
│   ├── coding-style.md
│   ├── git-workflow.md
│   ├── hooks.md
│   ├── patterns.md
│   ├── performance.md
│   ├── security.md
│   └── testing.md
└── tools/                     # 工具定义
    ├── search-tools/
    ├── validation-tools/
    └── file-tools/
```

## 组件说明

### Agents (专家代理)

Agent 是具有特定领域专业知识的独立执行单元。每个 Agent 由一个 `.md` 文件定义，包含：

- **角色定义**：Agent 的身份和职责
- **核心能力**：Agent 擅长的任务类型
- **工作流程**：Agent 执行任务的标准步骤
- **知识库引用**：关联的 Skills 目录

**创建新 Agent**：

1. 在 `agents/` 目录创建 `{agent-name}.md`
2. 在 `skills/` 创建对应的 `for-{agent-name}/` 知识库
3. 在 `plugin.json` 的 `agents` 数组中添加路径
4. 在 `rules/agents.md` 中添加使用指南

### Commands (用户命令)

Command 是用户可通过 `/` 前缀调用的快捷指令。每个 Command 由一个 `.md` 文件定义，包含：

- **命令名称**：文件名即命令名（如 `dev.md` 对应 `/dev`）
- **命令描述**：命令的功能说明
- **使用场景**：何时使用该命令
- **执行流程**：命令执行的步骤

**创建新 Command**：

1. 在 `commands/` 目录创建 `{command-name}.md`
2. 编写命令规范（参考现有 Command 格式）
3. 在 `plugin.json` 的 `commands` 数组中已包含整个目录，无需单独添加

### Skills (知识库)

Skills 是按领域专家组织的知识库。每个 Skill 目录包含：

```
for-{expert-name}/
├── SKILL.md                   # Skill 入口文档
├── architecture/              # 架构规范
├── references/                # 参考资料
│   ├── sop/                  # 标准作业流程
│   ├── methodology/          # 方法论
│   ├── principles/           # 原则
│   ├── patterns/             # 设计模式
│   ├── anti-patterns/        # 反模式
│   ├── checklists/           # 检查清单
│   ├── domain-knowledge/     # 领域知识
│   └── templates/            # 模板
└── tests/                     # 测试用例（可选）
```

**创建新 Skill**：

1. 在 `skills/` 创建 `for-{expert-name}/` 目录
2. 创建 `SKILL.md` 入口文档
3. 按需创建子目录（sop/methodology/patterns 等）
4. 在关联的 Agent 中引用该 Skill

### Rules (全局规则)

Rules 是应用到所有会话的全局行为规则。规则文件会被复制到用户的 `~/.claude/rules/` 目录。

**现有规则**：

- `agents.md`：子代理编排规则
- `architecture/`：架构分层规范
- `coding-style.md`：编码风格
- `git-workflow.md`：Git 工作流
- `security.md`：安全指南
- `testing.md`：测试要求

**添加新规则**：

1. 在 `rules/` 创建规则文件
2. 规则会在插件安装时自动生效
3. 用户可以在本地自定义覆盖

### Hooks (钩子脚本)

Hooks 是在特定事件触发时自动执行的脚本。详见 [HOOKS.md](./HOOKS.md)。

### Tools (工具定义)

Tools 是可被 Agent 调用的工具函数。每个工具目录包含：

- `README.md`：工具说明
- 工具实现文件

## 配置文件

### plugin.json

插件的元数据和配置信息：

```json
{
  "$schema": "https://anthropic.com/claude-code/plugin.schema.json",
  "name": "spec-compiler-kit",
  "displayName": "规格编译器套件",
  "version": "2.0.0",
  "description": "将模糊需求编译为确定性规格文档",
  "category": "workflow",
  "author": { "name": "zxq", "email": "zxq@example.com" },
  "homepage": "https://github.com/zxq/spec-compiler-kit",
  "repository": { "type": "git", "url": "https://github.com/zxq/spec-compiler-kit.git" },
  "license": "MIT",
  "keywords": ["spec", "compiler", "ddd", "modeling", "architecture", "tdd"],
  "engines": { "claude-code": ">=1.0.0" },
  "strict": false,
  "skills": ["./skills/"],
  "commands": ["./commands/"],
  "agents": ["./agents/"],
  "hooks": ["./.claude-plugin/hooks/"]
}
```

### marketplace.json

Marketplace 配置（用于本地开发和远程发布）：

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "spec-compiler-kit-marketplace",
  "owner": { "name": "zxq", "email": "zxq@example.com" },
  "metadata": {
    "description": "Spec Compiler Kit - 本地开发 Marketplace",
    "version": "1.0.0"
  },
  "plugins": [{
    "name": "spec-compiler-kit",
    "description": "规格编译器套件",
    "source": "./",
    "strict": false
  }]
}
```

## 开发工作流

### 1. 本地开发

```bash
# 1. 克隆项目
git clone https://github.com/zxq/spec-compiler-kit.git
cd spec-compiler-kit

# 2. 创建 local marketplace 链接
ln -s /path/to/spec-compiler-kit ~/.claude/plugins/local/spec-compiler-kit

# 3. 验证插件加载
claude-code --plugin list
```

### 2. 测试更改

```bash
# 修改 Agent/Skill 后，在 Claude Code 中测试
/agent help spec-compiler-v4
/skill help spec-compiler-v4
```

### 3. 版本发布

详见 [VERSIONING.md](./VERSIONING.md) 和 [PUBLISHING.md](./PUBLISHING.md)。

## 最佳实践

### Agent 设计

- **单一职责**：每个 Agent 专注于一个领域
- **明确边界**：清晰定义 Agent 的能力边界
- **可组合**：Agent 可以互相协作

### Skill 组织

- **层次结构**：使用 sop/methodology/patterns 分类
- **模板化**：提供可复用的代码模板
- **检查清单**：包含 QA 检查清单

### 命名规范

| 类型 | 命名模式 | 示例 |
|------|----------|------|
| Agent | `{role}-expert` 或 `{role}-{suffix}` | `java-expert`, `product-manager` |
| Skill | `for-{agent-name}` | `for-java-expert` |
| Command | `{action}-{scope}` | `dev-feature`, `test` |
| Hook | `{event}-{action}` | `phase-review-check` |

## 调试

### 查看插件状态

```bash
/plugin list
/plugin info spec-compiler-kit
```

### 查看组件加载

```bash
/agent list
/skill list
```

### 常见问题

1. **Agent 未加载**：检查 `plugin.json` 的 `agents` 路径
2. **Skill 未生效**：检查关联的 Agent 是否正确引用
3. **Command 不可用**：确认 `commands/` 目录在 `plugin.json` 中声明

## 贡献指南

1. Fork 项目
2. 创建功能分支
3. 遵循现有代码风格
4. 添加测试和文档
5. 提交 Pull Request

## 许可证

MIT License. 详见 LICENSE 文件。
