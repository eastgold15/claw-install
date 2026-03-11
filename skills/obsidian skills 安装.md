# 💎 Obsidian Skills 安装指南

> OpenClaw 的 Obsidian 技能安装与配置，实现智能笔记管理

## 📋 技能概述

Obsidian 技能让 OpenClaw 能够直接操作 Obsidian 笔记库，实现自动化的笔记管理、搜索、创建等功能。

## 🔗 官方资源

- **Obsidian 创始人的技能仓库**: https://github.com/kepano/obsidian-skills.git
- **ClawHub 技能页面**: https://clawhub.ai/steipete/obsidian

## 🚀 安装方法

### 方法一：使用 ClawHub 安装（推荐）

```bash
# 安装 Obsidian 技能
clawhub install obsidian

# 查看已安装技能
clawhub list

# 更新技能
clawhub update obsidian
```

### 方法二：手动安装

```bash
# 进入技能目录
cd ~/.openclaw/workspace/skills/

# 克隆技能仓库
git clone https://github.com/kepano/obsidian-skills.git obsidian

# 或从 ClawHub 下载
curl -fsSL https://clawhub.ai/steipete/obsidian/archive/main.tar.gz | tar -xz
```

## ⚙️ 配置要求

### 1. Obsidian CLI

Obsidian 1.12+ 版本内置了官方 CLI 工具：

1. **启用 CLI**:
   - 打开 Obsidian 应用
   - 进入 `Settings` → `General` → `Command line interface`
   - 勾选 "Enable command line interface"

2. **验证安装**:
```bash
obsidian --version
obsidian --help
```

### 2. 环境变量

确保以下环境变量已设置：

```bash
# 检查环境变量
echo $HOME

# Obsidian 配置目录（macOS/Linux）
ls ~/Library/Application\ Support/obsidian/

# Windows 配置目录
ls %APPDATA%\obsidian\
```

## 🛠️ 使用方法

### 基本命令

```bash
# 查看帮助
obsidian --help

# 打开笔记
obsidian "笔记名称"

# 创建新笔记
obsidian new "新笔记名称"

# 搜索笔记
obsidian search "搜索词"

# 搜索笔记内容
obsidian query "搜索内容"

# 列出所有 vault
obsidian vault list

# 打开今日日记
obsidian daily

# 查看所有标签
obsidian tags
```

### 高级操作

```bash
# 设置默认 vault
obsidian set-default "vault-name"

# 获取默认 vault 路径
obsidian print-default --path-only

# 搜索笔记内容
obsidian search-content "搜索词"

# 创建笔记并添加内容
obsidian create "新笔记" --content "笔记内容"

# 移动笔记（自动更新链接）
obsidian move "旧路径/笔记" "新路径/笔记"

# 删除笔记
obsidian delete "路径/笔记"
```

## 🔧 OpenClaw 集成

### 1. 技能配置

安装完成后，技能会自动集成到 OpenClaw 中。你可以通过以下方式使用：

```bash
# 在 OpenClaw 中使用 Obsidian 技能
openclaw obsidian search "搜索词"
openclaw obsidian create "新笔记"
```

### 2. 自动化工作流

创建自动化脚本 `auto-notes.sh`:

```bash
#!/bin/bash

# 创建今日日记
obsidian daily

# 添加待办事项
obsidian content="## 今日待办\n- [ ] 任务1\n- [ ] 任务2"

# 搜索相关笔记
obsidian search "项目A"
```

### 3. 与其他技能集成

- [[飞书配置.md]] - 将 Obsidian 笔记同步到飞书
- [[Obsidian 使用方法.md]] - 详细使用指南

## 🚨 常见问题

### 1. CLI 未启用

**问题**: `obsidian: command not found`

**解决方案**:
1. 确保安装了 Obsidian 1.12+
2. 在 Obsidian 设置中启用 CLI
3. 重启终端

### 2. Vault 未找到

**问题**: "No vault found" 或 "Vault not accessible"

**解决方案**:
1. 检查 Obsidian 配置文件
2. 确保 vault 路径正确
3. 设置默认 vault

### 3. 权限问题

**问题**: "Permission denied" 或 "Access denied"

**解决方案**:
1. 检查文件权限
2. 确保用户有读写权限
3. 检查 vault 配置

### 4. 链接更新失败

**问题**: 移动笔记后链接未更新

**解决方案**:
1. 使用 `obsidian move` 而非 `mv`
2. 确保启用了链接更新功能
3. 检查 vault 设置

## 🔗 相关链接

- [[📚 OpenClaw 知识库索引]] - 知识库主页
- [[Obsidian 使用方法.md]] - 详细使用指南
- [[安装.md]] - OpenClaw 安装指南
- [[飞书配置.md]] - 飞书集成配置

## 💡 最佳实践

### 1. 笔记结构
- 使用一致的命名规范
- 合理组织文件夹结构
- 利用标签和元数据

### 2. 链接管理
- 使用双链连接相关笔记
- 定期检查和修复断开的链接
- 利用图谱视图查看知识结构

### 3. 自动化
- 创建模板和快捷操作
- 设置定期备份
- 集成到日常工作流

### 4. 性能优化
- 定期清理不需要的笔记
- 优化搜索和查询
- 使用缓存提高性能

---

*Obsidian Skills 安装指南最后更新: 2026-03-12*