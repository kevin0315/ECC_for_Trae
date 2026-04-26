# Everything Claude Code for Trae

为 Trae IDE 带来 Everything Claude Code (ECC) 工作流。此仓库提供自定义命令、智能体、技能和规则，可以通过单个命令安装到任何 Trae 项目中。

## 快速开始

### 不同操作系统的安装命令

#### Linux/macOS (使用 bash)

```bash
# 安装到当前项目的 .trae 目录（默认环境）
cd /path/to/your/project
.trae/install.sh

# 安装到当前项目的 .trae-cn 目录（CN 环境）
cd /path/to/your/project
TRAE_ENV=cn .trae/install.sh

# 全局安装到 ~/.trae/（默认环境）
.trae/install.sh ~

# 全局安装到 ~/.trae-cn/（CN 环境）
TRAE_ENV=cn .trae/install.sh ~
```

#### Windows (使用 PowerShell)

```powershell
# 安装到当前项目的 .trae 目录（默认环境）
cd C:\path\to\your\project
.trae\install.sh

# 安装到当前项目的 .trae-cn 目录（CN 环境）
cd C:\path\to\your\project
$env:TRAE_ENV="cn"
.trae\install.sh

# 全局安装到 ~\.trae/（默认环境）
.trae\install.sh ~

# 全局安装到 ~\.trae-cn/（CN 环境）
$env:TRAE_ENV="cn"
.trae\install.sh ~
```

#### Windows (使用 Git Bash)

```bash
# 安装到当前项目的 .trae 目录（默认环境）
cd /c/path/to/your/project
.trae/install.sh

# 安装到当前项目的 .trae-cn 目录（CN 环境）
cd /c/path/to/your/project
TRAE_ENV=cn .trae/install.sh

# 全局安装到 ~/.trae/（默认环境）
.trae/install.sh ~

# 全局安装到 ~/.trae-cn/（CN 环境）
TRAE_ENV=cn .trae/install.sh ~
```

### 安装模式

### 本地安装

安装到当前项目的 `.trae` 或 `.trae-cn` 目录：

```bash
# 安装到当前项目的 .trae 目录（默认）
cd /path/to/your/project
.trae/install.sh

# 安装到当前项目的 .trae-cn 目录（CN 环境）
cd /path/to/your/project
TRAE_ENV=cn .trae/install.sh
```

### 全局安装

安装到您主目录的 `.trae` 或 `.trae-cn` 目录（适用于所有 Trae 项目）：

```bash
# 全局安装到 ~/.trae/（默认）
.trae/install.sh ~

# 全局安装到 ~/.trae-cn/（CN 环境）
TRAE_ENV=cn .trae/install.sh ~
```

**注意**：全局安装适用于希望在所有项目之间维护单个 ECC 副本的场景。

## 环境支持

- **默认**：使用 `.trae` 目录
- **CN 环境**：使用 `.trae-cn` 目录（通过 `TRAE_ENV=cn` 设置）

### 强制指定环境

```bash
# 从项目根目录强制使用 CN 环境
TRAE_ENV=cn .trae/install.sh

# 进入 .trae 目录后使用默认环境
cd .trae
./install.sh
```

**注意**：`TRAE_ENV` 是一个全局环境变量，适用于整个安装会话。

## 卸载

卸载程序使用清单文件（`.ecc-manifest`）跟踪已安装的文件，确保安全删除：

```bash
# 从当前目录卸载（如果已经在 .trae 或 .trae-cn 目录中）
cd .trae-cn
./uninstall.sh

# 或者从项目根目录卸载
cd /path/to/your/project
TRAE_ENV=cn .trae/uninstall.sh

# 从主目录全局卸载
TRAE_ENV=cn .trae/uninstall.sh ~

# 卸载前会询问确认
```

### 卸载行为

- **安全删除**：仅删除清单中跟踪的文件（由 ECC 安装的文件）
- **保留用户文件**：您手动添加的任何文件都会被保留
- **非空目录**：包含用户添加文件的目录会被跳过
- **基于清单**：需要 `.ecc-manifest` 文件（在安装时创建）

### 环境支持

卸载程序遵循与安装程序相同的 `TRAE_ENV` 环境变量：

```bash
# 从 .trae-cn 卸载（CN 环境）
TRAE_ENV=cn ./uninstall.sh

# 从 .trae 卸载（默认环境）
./uninstall.sh
```

**注意**：如果找不到清单文件（旧版本安装），卸载程序将询问是否删除整个目录。

## 包含的内容

### 上下文文件

- **TRAE.md** — 主要的 Trae 上下文文件，提供工作流指导、编码标准和安全检查清单
- **AGENTS.md** — Trae 特定的智能体说明和模型推荐

### 命令

命令是通过 Trae 聊天中的 `/` 菜单调用的按需工作流。所有命令都直接复用自项目根目录的 `commands/` 文件夹。

| 命令 | 用途 |
|------|------|
| `/plan` | 创建实施计划 |
| `/tdd` | 测试驱动开发 |
| `/code-review` | 质量审查 |
| `/build-fix` | 修复构建错误 |
| `/e2e` | 生成端到端测试 |
| `/verify` | 运行验证循环 |
| `/refactor-clean` | 移除死代码 |
| `/learn` | 提取模式 |

### 智能体

智能体是具有特定工具配置的专门 AI 助手。所有智能体都直接复用自项目根目录的 `agents/` 文件夹。

| 智能体 | 用途 | 使用场景 |
|--------|------|----------|
| `planner` | 实施规划 | 复杂功能 |
| `architect` | 系统设计 | 架构决策 |
| `tdd-guide` | 测试驱动开发 | 新功能、错误修复 |
| `code-reviewer` | 质量审查 | 编写代码后 |
| `security-reviewer` | 安全审计 | 提交前 |
| `go-reviewer` | Go 代码审查 | Go 项目 |
| `python-reviewer` | Python 代码审查 | Python 项目 |
| `rust-reviewer` | Rust 代码审查 | Rust 项目 |
| `typescript-reviewer` | TS/JS 审查 | TypeScript 项目 |

### 技能

技能是通过聊天中的 `/` 菜单调用的按需工作流。所有技能都直接复用自项目的 `skills/` 文件夹。

| 技能 | 用途 |
|------|------|
| `tdd-workflow` | TDD 方法论 |
| `security-review` | 安全检查清单 |
| `coding-standards` | 编码最佳实践 |
| `api-design` | REST API 模式 |
| `e2e-testing` | Playwright 端到端测试 |
| `eval-harness` | 评估框架 |

### 规则

规则提供始终适用的规则和上下文，塑造智能体处理代码的方式。所有规则都直接复用自项目根目录的 `rules/` 文件夹。

| 类别 | 文件 |
|------|------|
| 通用 | coding-style, git-workflow, testing, performance, patterns, hooks, agents, security |
| 语言特定 | typescript, python, golang, swift, php, java, kotlin, rust, cpp, csharp, dart, perl |

## 使用方法

1. 在聊天中输入 `/` 以打开命令菜单
2. 选择一个命令或技能
3. 智能体将通过具体说明和检查清单指导您完成工作流

## 项目结构

```
.trae/ (或 .trae-cn/)
├── TRAE.md           # Trae 上下文文件（工作流指导）
├── AGENTS.md        # Trae 智能体补充
├── commands/        # 72 个命令文件（复用自项目根目录）
├── agents/          # 38 个智能体文件（复用自项目根目录）
├── skills/          # 技能目录（复用自 skills/）
├── rules/           # 规则文件（复用自项目根目录）
├── install.sh       # 安装脚本
├── uninstall.sh     # 卸载脚本
└── README.md        # 本文件
```

## 工作原理

### 上下文加载

当 Trae 在安装了 ECC 的项目中启动会话时：

1. **TRAE.md** 被加载 — 提供 Trae 特定的工作流指导
2. **AGENTS.md** 被加载 — 提供智能体说明和模型推荐
3. **规则** 从 `rules/` 加载 — 提供始终遵循的指南

### 命令执行

当您通过 `/` 调用命令时：

1. Trae 从 `.trae/commands/` 读取命令文件
2. 命令提供工作流说明
3. 智能体执行具有特定步骤的工作流

### 智能体委托

对于复杂任务，使用智能体：

1. 分析任务并分配给适当的智能体
2. 智能体使用其专业工具和知识
3. 结果被综合回主会话

## 自定义

安装后，所有文件都归您修改。安装程序永远不会覆盖现有文件，因此您的自定义在重新安装时是安全的。

**注意**：安装时会自动将 `install.sh` 和 `uninstall.sh` 脚本复制到目标目录，这样您可以在项目本地直接运行这些命令。

## 推荐的工作流

1. **从计划开始**：使用 `/plan` 命令分解复杂功能
2. **先写测试**：在实现之前调用 `/tdd` 命令
3. **审查您的代码**：编写代码后使用 `/code-review`
4. **检查安全性**：对于身份验证、API 端点或敏感数据处理，再次使用 `/code-review`
5. **修复构建错误**：如果有构建错误，使用 `/build-fix`
6. **提交前验证**：使用 `/verify` 运行验证循环

## 编码标准

- **不可变性** - 始终创建新对象，永远不要改变现有对象
- **小函数** - 函数不超过 50 行，文件不超过 800 行
- **输入验证** - 在系统边界验证
- **错误处理** - 明确错误信息，失败时大声报错
- **无硬编码密钥** - 使用环境变量

## 安全检查清单

提交前：

- 无硬编码的 API 密钥、密码或令牌
- 所有外部输入都经过验证
- 数据库写入使用参数化查询
- 适当的地方对 HTML 输出进行清理
- 敏感路径检查授权/认证

## 测试要求

- **最低覆盖率：80%**
- 针对独立函数的单元测试
- 针对 API 端点的集成测试
- 针对关键用户流的端到端测试

## 使用教程

### 基础使用示例

#### 1. 开始一个新功能

**步骤：**

1. **规划功能**
   - 在 Trae 聊天中输入：`/plan "添加用户认证功能"`
   - 智能体会生成详细的实施计划

2. **编写测试**
   - 输入：`/tdd`
   - 按照智能体的指导编写测试用例

3. **实现代码**
   - 根据测试用例实现功能

4. **代码审查**
   - 输入：`/code-review`
   - 智能体会检查代码质量和安全性

5. **验证**
   - 输入：`/verify`
   - 运行完整的验证循环

#### 2. 修复构建错误

**步骤：**

1. **查看错误信息**
   - 在终端中看到构建错误

2. **使用 build-fix**
   - 在 Trae 聊天中输入：`/build-fix`
   - 智能体会分析错误并提供修复方案

3. **应用修复**
   - 按照智能体的建议修改代码

4. **验证修复**
   - 再次运行构建命令确认修复成功

#### 3. 安全审查

**步骤：**

1. **针对敏感代码**
   - 输入：`/code-review`
   - 智能体会检查安全漏洞

2. **检查 API 端点**
   - 针对 API 代码再次运行：`/code-review`
   - 智能体会检查认证、授权和输入验证

3. **修复安全问题**
   - 按照智能体的建议修复安全问题

### 高级使用场景

#### 1. 多语言项目

**场景：** 项目包含 TypeScript 和 Python 代码

**使用方法：**
- 对于 TypeScript 代码：`/code-review`（自动使用 typescript-reviewer 智能体）
- 对于 Python 代码：`/python-review`（使用 python-reviewer 智能体）

#### 2. 数据库优化

**场景：** 优化 PostgreSQL 查询性能

**使用方法：**
- 输入：`/plan "优化数据库查询性能"`
- 智能体会分析并提供优化建议
- 对于复杂查询，会自动委托给 database-reviewer 智能体

#### 3. 端到端测试

**场景：** 为用户注册流程创建 E2E 测试

**使用方法：**
- 输入：`/e2e "用户注册流程"`
- 智能体会生成 Playwright 测试代码
- 运行测试验证流程完整性

### 最佳实践

1. **保持会话简洁**
   - 完成一个任务后使用 `/clear` 重置会话
   - 在逻辑断点使用 `/compact` 压缩上下文

2. **合理使用智能体**
   - 复杂架构决策 → `architect` 智能体
   - 代码质量检查 → `code-reviewer` 智能体
   - 安全审计 → `security-reviewer` 智能体

3. **利用技能**
   - 测试驱动开发 → `tdd-workflow` 技能
   - API 设计 → `api-design` 技能
   - 安全检查 → `security-review` 技能

4. **定期验证**
   - 提交前运行 `/verify`
   - 定期运行 `/test-coverage` 检查覆盖率

## 下一步

- 在 Trae 中打开您的项目
- 输入 `/` 以查看可用命令
- 享受 ECC 工作流！
