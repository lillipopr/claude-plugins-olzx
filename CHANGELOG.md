# Changelog

本文档记录 Spec Compiler Kit 的所有重要变更。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

---

## [2.0.0] - 2026-01-31

### Added
- **插件化架构支持**
  - 完整的 `plugin.json` v2.0 配置规范
  - `marketplace.json` 配置支持
  - Hooks 体系架构和目录结构
  - 安装/卸载脚本支持
- **Hooks 体系**
  - PreToolUse hooks (Phase 审查闸口、架构分层检查)
  - PostToolUse hooks (规格一致性检查)
  - SessionStart/SessionEnd hooks
- **完整的开发文档**
  - `.claude-plugin/README.md` - 插件开发指南
  - `.claude-plugin/HOOKS.md` - Hooks 开发规范
  - `.claude-plugin/VERSIONING.md` - 版本管理规范
  - `.claude-plugin/PUBLISHING.md` - 发布流程指南
- **Scripts 支持**
  - `pre-install.sh` - 安装前检查
  - `post-install.sh` - 安装后初始化
  - `pre-uninstall.sh` - 卸载前清理

### Changed
- **重构 plugin.json 格式**
  - 添加 `$schema` 声明
  - 添加 `displayName` 字段
  - 添加 `repository` 对象格式
  - 添加 `bugs` 链接
  - 添加 `engines` 兼容性声明
  - 添加 `strict` 模式配置
  - 添加 `hooks` 路径声明
  - 添加 `dependencies` 和 `peerDependencies`
  - 添加 `scripts` 生命周期钩子
  - 添加 `features` 特性开关
  - 添加 `config` 默认配置
- **优化 agents 声明方式**
  - 从数组改为目录声明 `["./agents/"]`
  - 支持动态发现

### Breaking Changes
- **plugin.json 格式不兼容 v1.x**
  - 新增必需字段：`$schema`, `displayName`
  - `agents` 格式变更：从数组改为目录声明
  - 旧版本需要手动升级配置
- **目录结构变更**
  - 新增 `.claude-plugin/hooks/` 目录
  - 新增 `.claude-plugin/scripts/` 目录

### Migration Guide
从 v1.x 升级到 v2.0.0：

1. 备份当前配置
2. 拉取最新代码
3. 按照 plugin.json 新格式调整
4. 重新安装插件

详见 `.claude-plugin/VERSIONING.md` 升级指南。

---

## [1.0.0] - 2026-01-15

### Added
- **初始版本发布**
- **7 个领域专家 Agent**
  - `planner` - 实现规划
  - `domain-architect` - DDD 领域建模
  - `product-manager` - 产品需求分析
  - `spec-compiler-v4` - 规格编译器（4 Phase 流程）
  - `java-expert` - Java/后端专家
  - `ios-expert` - iOS/Swift 专家
  - `frontend-expert` - 前端专家
  - `tdd-expert` - TDD 专家
- **规格编译器核心功能**
  - Phase 1: 实体抽取
  - Phase 2: 用例推导
  - Phase 3: 跨端统一建模
  - Phase 4: 端到端接口串联
- **跨端架构支持**
  - Java DDD 分层架构
  - iOS MVVM 分层架构
  - Vue 3 前端分层架构
- **完整知识库**
  - SOP 标准作业流程
  - 方法论文档
  - 设计原则和模式
  - 代码模板
  - 检查清单

---

## 版本说明

### 版本格式
```
MAJOR.MINOR.PATCH

例如: 2.0.0
- MAJOR: 不兼容的 API 变更
- MINOR: 向后兼容的功能新增
- PATCH: 向后兼容的问题修复
```

### 变更类型
- **Added**: 新增功能
- **Changed**: 现有功能的变更
- **Deprecated**: 即将移除的功能
- **Removed**: 已移除的功能
- **Fixed**: 问题修复
- **Security**: 安全修复

---

## 链接

- [当前版本](../../releases/tag/v2.0.0)
- [所有版本](../../releases)
- [升级指南](.claude-plugin/VERSIONING.md)
