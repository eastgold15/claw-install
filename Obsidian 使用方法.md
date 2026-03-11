# Obsidian 使用方法

## 📋 基本信息
- **技能名称**: Obsidian
- **安装状态**: ✅ 已安装
- **安装位置**: `C:\Users\boer\.openclaw\workspace\skills\obsidian`
- **版本**: 1.0.0
- **安装时间**: 2026-03-12 00:59

## 🔧 安装与配置

### 1. 启用 Obsidian CLI
Obsidian 1.12+ 版本已经内置了官方 CLI 工具：

1. **打开 Obsidian 应用**
2. **进入设置**: `Settings` → `General` → `Command line interface`
3. **启用 CLI**: 勾选 "Enable command line interface" 选项
4. **验证安装**: 在终端中运行 `obsidian --version`

### 2. 依赖包
- ✅ obsidian-cli-mcp 已安装（MCP 服务器）

## 🚀 基本使用方法

### 常用命令
```bash
# 基本操作
obsidian --help                    # 查看帮助
obsidian --version                 # 查看版本

# 笔记操作
obsidian "今天的工作"              # 打开笔记
obsidian new "新笔记"              # 创建新笔记
obsidian search "查询词"           # 搜索笔记
obsidian query "搜索内容"          # 搜索笔记内容

# 高级操作
obsidian vault list               # 列出所有 vault
obsidian daily                    # 打开今日日记
obsidian tags                     # 查看所有标签
```

### Vault 管理
- **查找活跃的 vault**: 检查 `~/Library/Application Support/obsidian/obsidian.json`
- **设置默认 vault**: `obsidian-cli set-default "<vault-folder-name>"`
- **获取 vault 路径**: `obsidian-cli print-default --path-only`

### 笔记操作
- **搜索笔记**: `obsidian-cli search "查询词"`
- **搜索内容**: `obsidian-cli search-content "查询词"`
- **创建笔记**: `obsidian-cli create "文件夹/新笔记" --content "内容"`
- **移动重命名**: `obsidian-cli move "旧路径" "新路径"`（自动更新链接）
- **删除笔记**: `obsidian-cli delete "路径/笔记"`

## 💡 技能功能

### 主要能力
1. **自动化笔记管理**: 创建、编辑、移动笔记
2. **智能搜索**: 快速查找笔记内容
3. **批量操作**: 处理大量笔记
4. **集成工作流**: 与其他工具配合使用

### 适用场景
- **知识管理**: 系统化整理笔记
- **文档自动化**: 批量处理文档
- **工作流集成**: 与其他工具配合
- **内容创作**: 快速创建和编辑内容

## ⚠️ 注意事项

1. **Obsidian 应用必须运行**: CLI 工具需要 Obsidian 应用在后台运行
2. **Vault 结构**: 
   - 笔记: `*.md` (纯文本 Markdown)
   - 配置: `.obsidian/` (工作区和插件设置)
   - 画布: `*.canvas` (JSON)
   - 附件: 在 Obsidian 设置中选择的文件夹
3. **避免硬编码路径**: 优先读取配置或使用 `print-default`
4. **多个 vault**: 常见情况（iCloud vs `~/Documents`, 工作/个人等），不要猜测，读取配置

## 🔗 相关链接

- **官方文档**: https://obsidian.md/cli
- **帮助文档**: https://help.obsidian.md
- **技能来源**: https://clawhub.ai/steipete/obsidian

## 📝 更新记录

- **2026-03-12 01:05**: 初始创建，记录基本安装和使用方法