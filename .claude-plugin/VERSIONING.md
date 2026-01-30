# 版本管理规范

## 版本号格式

Spec Compiler Kit 遵循 [语义化版本 2.0.0](https://semver.org/lang/zh-CN/)：

```
MAJOR.MINOR.PATCH

例如: 2.0.0
- MAJOR: 不兼容的 API 变更
- MINOR: 向后兼容的功能新增
- PATCH: 向后兼容的问题修复
```

## 版本号示例

| 版本 | 类型 | 说明 |
|------|------|------|
| 2.0.0 | Major | 插件化架构重构，不兼容 v1.x |
| 2.1.0 | Minor | 新增 Hooks 支持 |
| 2.1.1 | Patch | 修复 Hook 加载问题 |
| 2.2.0 | Minor | 新增 Commands 支持 |
| 3.0.0 | Major | 重大架构变更 |

## 变更类型分类

### Major 变更（不兼容）

需要升级主版本号的变更：

1. **配置格式变更**
   - `plugin.json` 结构变化
   - 必需字段变更
   - 字段类型变更

2. **目录结构变更**
   - 删除或重命名核心目录
   - 移动关键文件位置

3. **Agent 接口变更**
   - 删除现有 Agent
   - Agent 输入/输出格式变化

4. **Hook 接口变更**
   - Hook 类型变更
   - Hook 配置格式变化

### Minor 变更（向后兼容）

需要升级次版本号的变更：

1. **新增功能**
   - 添加新 Agent
   - 添加新 Skill
   - 添加新 Command
   - 添加新 Hook

2. **新增配置选项**
   - 在 `plugin.json` 添加可选字段
   - 添加新的 Hook 配置

3. **知识库扩展**
   - 添加新的方法论文档
   - 添加新的代码模板

### Patch 变更（问题修复）

需要升级修订号的变更：

1. **Bug 修复**
   - 修复 Agent 执行逻辑
   - 修复 Skill 内容错误
   - 修复 Hook 触发条件

2. **文档改进**
   - 修正文档错误
   - 添加文档说明
   - 改进示例代码

3. **性能优化**
   - 优化 Hook 执行性能
   - 减少资源占用

## 发布流程

### 1. 版本规划

在发布新版本前，确定：

- [ ] 版本号（MAJOR.MINOR.PATCH）
- [ ] 变更类型（Major/Minor/Patch）
- [ ] 变更内容摘要
- [ ] 是否有破坏性变更

### 2. 更新版本号

**方式一：手动更新**

编辑 `plugin.json`：

```json
{
  "name": "spec-compiler-kit",
  "version": "2.0.0"  // 更新此处
}
```

**方式二：使用版本管理命令**

```bash
# 创建版本分支
git checkout -b release/2.0.0

# 更新版本号
npm version 2.0.0  # 如果使用 npm
# 或手动编辑 plugin.json

# 提交
git add plugin.json
git commit -m "chore: bump version to 2.0.0"
```

### 3. 更新 CHANGELOG

在项目根目录创建/更新 `CHANGELOG.md`：

```markdown
# Changelog

## [2.0.0] - 2026-01-31

### Added
- 插件化架构支持
- Hooks 体系
- 完整的开发文档

### Changed
- 重构 plugin.json 格式
- 重新组织目录结构

### Fixed
- 修复 Agent 加载问题

### Breaking Changes
- plugin.json 格式不兼容 v1.x
- 需要重新配置 marketplace

## [1.0.0] - 2026-01-15

### Added
- 初始版本
- 7 个领域专家 Agent
- 规格编译器核心功能
```

### 4. 创建 Git Tag

```bash
# 创建 annotated tag
git tag -a v2.0.0 -m "Release v2.0.0: 插件化架构"

# 推送 tag
git push origin v2.0.0

# 或推送所有 tags
git push origin --tags
```

### 5. 发布 GitHub Release

1. 访问 GitHub Releases 页面
2. 点击 "Draft a new release"
3. 选择刚创建的 tag (v2.0.0)
4. 填写 Release Title: `v2.0.0 - 插件化架构`
5. 填写 Release Notes（从 CHANGELOG 复制）
6. 点击 "Publish release"

### 6. 更新 Marketplace

如果插件已发布到 Marketplace：

```bash
# 更新 marketplace.json 中的版本号
{
  "plugins": [{
    "name": "spec-compiler-kit",
    "version": "2.0.0"  // 更新
  }]
}

# 提交并推送
git add .claude-plugin/marketplace.json
git commit -m "chore: update marketplace version to 2.0.0"
git push
```

## 预发布版本

对于不稳定版本，可以使用预发布标识：

```
2.0.0-alpha.1
2.0.0-beta.1
2.0.0-rc.1
```

| 标识 | 用途 | 稳定性 |
|------|------|--------|
| alpha | 内部测试，功能不完整 | 极低 |
| beta | 功能完整，有已知问题 | 低 |
| rc (Release Candidate) | 候选版本，等待最终测试 | 中 |

### 预发布版本示例

```bash
# Alpha 版本
git tag -a v2.0.0-alpha.1 -m "Alpha 1: 插件化架构"

# Beta 版本
git tag -a v2.0.0-beta.1 -m "Beta 1: 功能完整，等待测试"

# RC 版本
git tag -a v2.0.0-rc.1 -m "RC 1: 候选发布版本"
```

## 版本兼容性

### 依赖声明

在 `plugin.json` 中声明依赖：

```json
{
  "engines": {
    "claude-code": ">=1.0.0"
  },
  "dependencies": {
    "optional-plugin": ">=1.0.0 <2.0.0"
  }
}
```

### 兼容性矩阵

| Spec Compiler Kit | Claude Code | 兼容性 |
|-------------------|-------------|--------|
| 1.x | >= 0.5.0 | ✅ 完全兼容 |
| 2.0.0 | >= 1.0.0 | ✅ 需要 Claude Code 1.0+ |
| 2.x | >= 1.0.0 | ✅ 完全兼容 |

## 升级指南

### 从 v1.x 升级到 v2.0.0

#### 破坏性变更

1. **plugin.json 格式变更**

```diff
{
- "skills": ["./skills/"],
- "commands": ["./commands/"],
- "agents": ["./agents/*.md"]
+ "skills": ["./skills/"],
+ "commands": ["./commands/"],
+ "agents": ["./agents/"],
+ "hooks": ["./.claude-plugin/hooks/"]
}
```

2. **目录结构变更**

```
新增：
.claude-plugin/hooks/
.claude-plugin/scripts/
```

#### 升级步骤

```bash
# 1. 备份当前配置
cp plugin.json plugin.json.bak

# 2. 拉取最新代码
git pull origin main

# 3. 更新本地配置
# 按照 plugin.json 新格式调整

# 4. 重新安装插件
/plugin uninstall spec-compiler-kit
/plugin install spec-compiler-kit

# 5. 验证
/plugin list
```

## 分支策略

```
main (生产分支)
  ↑
  └─ release/* (发布分支)
        ↑
        └─ develop (开发分支)
              ↑
              ├─ feature/* (功能分支)
              ├─ fix/* (修复分支)
              └─ hotfix/* (紧急修复)
```

### 分支命名

| 分支类型 | 命名模式 | 示例 |
|----------|----------|------|
| 功能开发 | `feature/` | `feature/hooks-support` |
| 问题修复 | `fix/` | `fix/hook-loading` |
| 紧急修复 | `hotfix/` | `hotfix/critical-bug` |
| 发布准备 | `release/` | `release/2.0.0` |

## 发布检查清单

发布前检查：

- [ ] 版本号已更新
- [ ] CHANGELOG 已更新
- [ ] 所有测试通过
- [ ] 文档已同步更新
- [ ] 破坏性变更已记录
- [ ] Git tag 已创建
- [ ] GitHub Release 已发布

## 版本回退

如果发现严重问题需要回退：

```bash
# 1. 回退到上一个版本
git revert HEAD

# 2. 或者强制重置（谨慎使用）
git reset --hard v1.0.0
git push --force

# 3. 发布新的修复版本
git tag -a v2.0.1 -m "Hotfix: 修复 v2.0.0 严重问题"
```

## 相关文档

- [README.md](./README.md) - 插件开发指南
- [HOOKS.md](./HOOKS.md) - Hooks 开发规范
- [PUBLISHING.md](./PUBLISHING.md) - 发布流程指南
