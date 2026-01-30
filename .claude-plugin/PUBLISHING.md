# 发布流程指南

## 概述

本文档描述如何将 Spec Compiler Kit 发布为 Claude Code 插件，供其他用户安装使用。

## 发布方式

Spec Compiler Kit 支持三种发布方式：

| 方式 | 复杂度 | 适用场景 |
|------|--------|----------|
| **Local Marketplace** | 低 | 个人使用、团队内部 |
| **Public Marketplace** | 中 | 公开发布、社区贡献 |
| **Direct Install** | 低 | 快速分享、临时安装 |

---

## 方式一：Local Marketplace（本地开发）

### 适用场景

- 本地开发测试
- 团队内部共享

### 配置步骤

#### 1. 创建 Local Marketplace

在用户本地创建 marketplace：

```bash
# 创建本地 marketplace 目录
mkdir -p ~/.claude/plugins/local/.claude-plugin

# 创建 marketplace.json
cat > ~/.claude/plugins/local/.claude-plugin/marketplace.json << 'EOF'
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "local",
  "description": "Local plugins directory for development",
  "owner": {
    "name": "your-name",
    "email": "your-email@example.com"
  },
  "plugins": [
    {
      "name": "spec-compiler-kit",
      "description": "规格编译器套件",
      "version": "2.0.0",
      "source": "./spec-compiler-kit",
      "category": "workflow"
    }
  ]
}
EOF

# 创建符号链接到插件目录
ln -s /path/to/spec-compiler-kit ~/.claude/plugins/local/spec-compiler-kit
```

#### 2. 验证安装

在 Claude Code 中运行：

```
/plugin list
```

应该看到 `spec-compiler-kit` 已列出。

---

## 方式二：Public Marketplace（公开发布）

### 适用场景

- 向社区公开发布
- 支持一键安装
- 版本管理和更新

### 准备工作

#### 1. 创建 Marketplace 仓库

创建独立的市场仓库 `spec-compiler-plugins`：

```bash
# 创建新仓库
mkdir spec-compiler-plugins
cd spec-compiler-plugins
git init

# 创建 marketplace.json
cat > .claude-plugin/marketplace.json << 'EOF'
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "spec-compiler-plugins",
  "owner": {
    "name": "zxq",
    "email": "zxq@example.com"
  },
  "metadata": {
    "description": "Spec Compiler Kit 官方插件仓库",
    "version": "1.0.0"
  },
  "plugins": [
    {
      "name": "spec-compiler-kit",
      "description": "规格编译器套件：将模糊需求编译为确定性规格文档",
      "source": "./spec-compiler-kit"
    }
  ]
}
EOF

# 添加子模块（插件本体）
git submodule add https://github.com/zxq/spec-compiler-kit.git spec-compiler-kit

# 提交
git add .
git commit -m "Initial marketplace setup"
git branch -M main
git push origin main
```

#### 2. 目录结构

```
spec-compiler-plugins/
├── .claude-plugin/
│   └── marketplace.json       # Marketplace 配置
├── spec-compiler-kit/         # 子模块（插件本体）
│   ├── .claude-plugin/
│   │   └── plugin.json
│   ├── agents/
│   ├── commands/
│   ├── skills/
│   └── ...
├── README.md
└── LICENSE
```

### 发布流程

#### Step 1: 更新插件版本

在 `spec-compiler-kit` 仓库中：

```bash
# 更新 plugin.json 版本号
# 编辑 plugin.json: "version": "2.0.0"

# 提交
git add plugin.json
git commit -m "chore: bump version to 2.0.0"

# 创建 tag
git tag -a v2.0.0 -m "Release v2.0.0"
git push origin main --tags
```

#### Step 2: 更新 Marketplace 子模块

在 `spec-compiler-plugins` 仓库中：

```bash
# 更新子模块到最新版本
cd spec-compiler-kit
git pull origin main
git checkout v2.0.0
cd ..

# 提交子模块更新
git add spec-compiler-kit
git commit -m "chore: update spec-compiler-kit to v2.0.0"

# 创建 marketplace tag
git tag -a marketplace-v1.0.0 -m "Marketplace release v1.0.0"
git push origin main --tags
```

#### Step 3: 用户安装

用户可以通过以下命令安装：

```bash
# 添加 Marketplace
/plugin marketplace add https://github.com/zxq/spec-compiler-plugins

# 安装插件
/plugin install spec-compiler-kit

# 验证安装
/plugin list
```

---

## 方式三：Direct Install（直接安装）

### 适用场景

- 快速分享
- 不需要 Marketplace
- 临时安装

### 安装方法

用户可以直接从 GitHub 安装：

```bash
# Claude Code 会自动处理
/plugin install https://github.com/zxq/spec-compiler-kit
```

### 目录要求

直接安装时，仓库根目录必须包含：

```
spec-compiler-kit/
├── .claude-plugin/
│   └── plugin.json           # 必需
├── agents/                    # 可选
├── commands/                  # 可选
└── skills/                    # 可选
```

---

## 版本更新流程

### 场景：发布新版本 v2.1.0

```bash
# ===== 1. 更新插件本体 =====
cd spec-compiler-kit

# 1.1 更新版本号
# 编辑 plugin.json: "version": "2.1.0"
# 更新 CHANGELOG.md

# 1.2 提交并打 tag
git add plugin.json CHANGELOG.md
git commit -m "chore: release v2.1.0"
git tag -a v2.1.0 -m "Release v2.1.0"
git push origin main --tags

# ===== 2. 更新 Marketplace（如果使用）=====
cd ../spec-compiler-plugins

# 2.1 更新子模块
cd spec-compiler-kit
git fetch origin
git checkout v2.1.0
cd ..

# 2.2 提交更新
git add spec-compiler-kit
git commit -m "chore: update spec-compiler-kit to v2.1.0"

# 2.3 更新 marketplace.json（可选）
# 如果需要更新 marketplace 版本号
git add .claude-plugin/marketplace.json
git commit -m "chore: bump marketplace version"

git push origin main
```

### 用户更新

```bash
# 用户更新已安装的插件
/plugin update spec-compiler-kit
```

---

## 发布检查清单

### 发布前检查

- [ ] `plugin.json` 版本号已更新
- [ ] `CHANGELOG.md` 已更新
- [ ] 所有新增 Agent/Skill/Command 已在配置中声明
- [ ] 文档（README、HOOKS、VERSIONING）已同步更新
- [ ] 破坏性变更已记录
- [ ] 本地测试通过

### 发布中检查

- [ ] Git tag 已创建并推送
- [ ] GitHub Release 已发布
- [ ] Marketplace 子模块已更新（如适用）
- [ ] `marketplace.json` 版本号已更新（如适用）

### 发布后验证

- [ ] 新安装测试（全新环境）
- [ ] 升级测试（从旧版本升级）
- [ ] 所有 Agent 可用
- [ ] 所有 Skill 可加载
- [ ] 所有 Command 可执行

---

## 常见问题

### Q1: 插件安装后无法加载？

**A:** 检查以下几点：

1. `plugin.json` 格式是否正确
2. `skills`/`commands`/`agents` 路径是否正确
3. 是否有语法错误（JSON 格式）

### Q2: Marketplace 添加后看不到插件？

**A:** 确保：

1. `marketplace.json` 格式正确
2. `plugins` 数组中 `source` 路径正确
3. Marketplace 仓库可公开访问

### Q3: 子模块更新后用户看不到新版本？

**A:** 用户需要：

1. 运行 `/plugin update {plugin-name}`
2. 或卸载后重新安装

### Q4: 如何发布预发布版本（alpha/beta/rc）？

**A:** 使用预发布标识：

```bash
git tag -a v2.0.0-beta.1 -m "Beta 1"
git push origin v2.0.0-beta.1
```

用户可以选择安装预发布版本。

---

## 安全考虑

### 1. 访问控制

- 敏感插件使用私有仓库
- 限制 Marketplace 访问权限
- 使用 GitHub Teams 管理访问

### 2. 代码审查

- 所有变更需要 Pull Request
- 至少一人审查批准
- 检查恶意代码注入

### 3. 签名验证

（未来支持）考虑使用 GPG 签名验证插件完整性。

---

## 监控和反馈

### 安装统计

（未来支持）通过 GitHub Insights 或独立服务跟踪安装数量。

### 用户反馈

- GitHub Issues
- Discussions
- 社区论坛

### Bug 报告

模板化 Issue 报告：

```markdown
## Bug 描述
简要描述问题

## 环境信息
- Claude Code 版本:
- Spec Compiler Kit 版本:
- 操作系统:

## 复现步骤
1. 步骤一
2. 步骤二

## 期望行为
描述期望的行为

## 实际行为
描述实际发生的行为

## 日志
```
相关日志输出
```
```

---

## 相关文档

- [README.md](./README.md) - 插件开发指南
- [HOOKS.md](./HOOKS.md) - Hooks 开发规范
- [VERSIONING.md](./VERSIONING.md) - 版本管理规范
