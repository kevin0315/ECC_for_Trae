# ECC for Trae

基于Everything Claude Code (ECC) 的基础上，修改为适用于 Trae 的commant、Agent、skill和RULES工作流。此仓库提供自定义命令、智能体、技能和规则，可以通过单个命令安装到任何 Trae 项目中。

该项目目录结构：

```
ECC_for_Trae-v20260425/
├── .trae/                          # Trae IDE 配置目录
│
├── agents/                         # AI Agent 定义
│   ├── planner                     # 规划 Agent
│   ├── architect                   # 架构设计 Agent
│   ├── tdd-guide                   # TDD 指导 Agent
│   ├── code-reviewer               # 代码审查 Agent
│   ├── security-reviewer           # 安全审查 Agent
│   ├── build-error-resolver        # 构建错误解决 Agent
│   ├── e2e-runner                  # E2E 测试 Agent
│   ├── refactor-cleaner            # 代码清理 Agent
│   ├── doc-updater                 # 文档更新 Agent
│   ├── rust-reviewer               # Rust 代码审查 Agent
│   └── ... (其他语言专用 Agent)
│
├── commands/                       # 自定义命令
│
├── contexts/                       # 上下文配置
│
├── hooks/                          # 钩子脚本
│   ├── pre-tool-use/               # 工具使用前钩子
│   └── post-tool-use/              # 工具使用后钩子
│
├── mcp-configs/                    # MCP (Model Context Protocol) 配置
│
├── rules/                          # 开发规则和规范
│   ├── common/                     # 通用规则 (语言无关)
│   │   ├── coding-style.md         # 编码风格
│   │   ├── git-workflow.md         # Git 工作流
│   │   ├── testing.md              # 测试规范
│   │   ├── performance.md          # 性能优化
│   │   ├── patterns.md             # 设计模式
│   │   ├── hooks.md                # 钩子系统
│   │   ├── agents.md               # Agent 编排
│   │   ├── security.md             # 安全指南
│   │   ├── code-review.md          # 代码审查标准
│   │   └── development-workflow.md # 开发工作流
│   ├── python/                     # Python 专用规则
│   ├── typescript/                 # TypeScript 专用规则
│   ├── golang/                     # Go 专用规则
│   ├── java/                       # Java 专用规则
│   ├── kotlin/                     # Kotlin 专用规则
│   ├── rust/                       # Rust 专用规则
│   ├── swift/                      # Swift 专用规则
│   ├── php/                        # PHP 专用规则
│   ├── cpp/                        # C++ 专用规则
│   ├── csharp/                     # C# 专用规则
│   ├── dart/                       # Dart 专用规则
│   ├── perl/                       # Perl 专用规则
│   ├── web/                        # Web/前端专用规则
│   └── zh/                         # 中文规则
│
├── schemas/                        # JSON Schema 定义
│
├── scripts/                        # 脚本工具
│   ├── ci/                         # CI/CD 脚本
│   ├── codemaps/                   # 代码映射脚本
│   ├── hooks/                      # 钩子脚本
│   └── lib/                        # 脚本库
│       ├── install/                # 安装脚本
│       ├── install-targets/        # 安装目标
│       ├── session-adapters/       # 会话适配器
│       ├── skill-evolution/        # Skill 演进脚本
│       ├── skill-improvement/      # Skill 改进脚本
│       └── state-store/            # 状态存储脚本
│
├── skills/                         # Skill 定义 (共 150+ 个)
│   ├── agent-eval/                 # Agent 评估
│   ├── agent-harness-construction/ # Agent 构建工具
│   ├── agentic-engineering/        # 代理工程
│   ├── ai-first-engineering/       # AI 优先工程
│   ├── api-design/                 # API 设计
│   ├── backend-patterns/           # 后端模式
│   ├── frontend-patterns/          # 前端模式
│   ├── python-patterns/            # Python 模式
│   ├── python-testing/             # Python 测试
│   ├── springboot-patterns/        # Spring Boot 模式
│   ├── django-patterns/            # Django 模式
│   ├── docker-patterns/            # Docker 模式
│   ├── git-workflow/               # Git 工作流
│   ├── tdd-workflow/               # TDD 工作流
│   ├── code-review/                # 代码审查
│   ├── security-review/            # 安全审查
│   ├── security-scan/              # 安全扫描
│   ├── deep-research/              # 深度研究
│   ├── market-research/            # 市场研究
│   ├── article-writing/            # 文章写作
│   ├── content-engine/             # 内容引擎
│   ├── ... (更多 Skill)
│   └── x-api/                      # X/Twitter API
│
├── tests/                          # 测试目录
│   ├── ci/                         # CI 测试
│   ├── hooks/                      # 钩子测试
│   ├── integration/                # 集成测试
│   ├── lib/                        # 库测试
│   ├── scripts/                    # 脚本测试
│   ├── codex-config.test.js
│   ├── opencode-config.test.js
│   ├── plugin-manifest.test.js
│   └── run-all.js
│
├── README.zh-CN.md                 # 中文说明文档
├── the-longform-guide.md           # 长文本指南
├── the-security-guide.md           # 安全指南
├── the-shortform-guide.md          # 短文本指南
└── yarn.lock                       # 依赖锁定文件
```

## 核心组件说明：

| 目录     | 作用                                       |
| -------- | ------------------------------------------ |
| agents/  | 定义各种 AI Agent 的角色和行为             |
| rules/   | 分层规则系统：common (通用) + 语言专用规则 |
| skills/  | 150+ 个专用 Skill，覆盖各种开发任务        |
| hooks/   | 自动化工具使用前后的钩子                   |
| scripts/ | 安装、配置、维护脚本                       |
| tests/   | 测试套件，确保规则和技能质量               |

## 快速开始

这里重点说明在trae通过ssh远程到linux系统，如何实现项目或普通用户全局导入的操作。

### 安装在项目中

安装到当前项目的 .trae 目录（默认环境），以下操作均在**项目目录**下完成。

#### Linux/macOS (使用 bash)

```bash
# 将ECC_for_Trae_v20260425.tar.bz2源码包上传到项目目录，并解压。
tar xvf ECC_for_Trae_v20260425.tar.bz2
# 解压后在项目目录下生成ECC_for_Trae-v20260425目录
# 修改ECC_for_Trae-v20260425/.trae/install.sh文件为可执行权限
chmod a+x ECC_for_Trae-v20260425/.trae/install.sh
# 在项目目录下执行如下命令安装
ECC_for_Trae-v20260425/.trae/install.sh
# 安装输出如下示例：
==========================================================================================================================
ECC Trae Installer
==================

Source:  /home/fastapi/fastapi_study/ECC_for_Trae-v20260425
Target:  /home/fastapi/fastapi_study/.trae/

Installation complete!

Components installed:
  Commands:  72
  Agents:    38
  Skills:    156
  Rules:     89

Directory:   .trae

Next steps:
  1. Open your project in Trae
  2. Type / to see available commands
  3. Enjoy the ECC workflows!

To uninstall later:
  cd /home/fastapi/fastapi_study/.trae
  ./uninstall.sh
==========================================================================================================================
# 在项目目录下的.trae目录出现如下目录和文件
drwxrwxr-x   2 fastapi fastapi  4096 Apr 26 19:17 agents
drwxrwxr-x   2 fastapi fastapi  4096 Apr 26 19:17 commands
-rwxrwxr-x   1 fastapi fastapi  6830 Apr 26 19:17 install.sh
-rw-rw-r--   1 fastapi fastapi  8796 Apr 26 19:17 README.md
-rw-rw-r--   1 fastapi fastapi 11447 Apr 26 19:17 README.zh-CN.md
drwxrwxr-x  17 fastapi fastapi  4096 Apr 26 19:17 rules
drwxrwxr-x 158 fastapi fastapi  8192 Apr 26 19:17 skills
-rwxrwxr-x   1 fastapi fastapi  5660 Apr 26 19:17 uninstall.sh
```

> 如果Trae默认是.trae-cn 目录，则需声明TRAE_ENV=cn，执行安装命令
>
> ```bash
> TRAE_ENV=cn ECC_for_Trae-v20260425/.trae/install.sh
> ```
>
> 其它安装步骤与.trae安装步骤一致。

### 安装在用户全局中

在trae通过ssh登录到Linux服务器后，在用户目录下会自动创建.trae或.trae-cn目录。

除了运行安装命令的目录有差异外，其安装过程与项目安装一致。

**以下操作皆在用户根目录下完成**

```bash
# 将ECC_for_Trae_v20260425.tar.bz2源码包上传到登录账号主目录，并解压。
tar xvf ECC_for_Trae_v20260425.tar.bz2
# 解压后在项目目录下生成ECC_for_Trae-v20260425目录
# 修改ECC_for_Trae-v20260425/.trae/install.sh文件为可执行权限
chmod a+x ECC_for_Trae-v20260425/.trae/install.sh
# 在项目目录下执行如下命令安装
ECC_for_Trae-v20260425/.trae/install.sh
# 安装输出如下示例：
==========================================================================================================================
ECC Trae Installer
==================

Source:  /home/fastapi/ECC_for_Trae-v20260425
Target:  /home/fastapi/.trae/

Installation complete!

Components installed:
  Commands:  72
  Agents:    38
  Skills:    156
  Rules:     89

Directory:   .trae

Next steps:
  1. Open your project in Trae
  2. Type / to see available commands
  3. Enjoy the ECC workflows!

To uninstall later:
  cd /home/fastapi/.trae
  ./uninstall.sh
==========================================================================================================================
# 在项目目录下的.trae目录出现如下目录和文件
drwxrwxr-x   2 fastapi fastapi  4096 Apr 26 19:17 agents
drwxrwxr-x   2 fastapi fastapi  4096 Apr 26 19:17 commands
-rwxrwxr-x   1 fastapi fastapi  6830 Apr 26 19:17 install.sh
-rw-rw-r--   1 fastapi fastapi  8796 Apr 26 19:17 README.md
-rw-rw-r--   1 fastapi fastapi 11447 Apr 26 19:17 README.zh-CN.md
drwxrwxr-x  17 fastapi fastapi  4096 Apr 26 19:17 rules
drwxrwxr-x 158 fastapi fastapi  8192 Apr 26 19:17 skills
-rwxrwxr-x   1 fastapi fastapi  5660 Apr 26 19:17 uninstall.sh
```

> 如果Trae默认是.trae-cn 目录，则需声明TRAE_ENV=cn，执行安装命令
>
> ```bash
> TRAE_ENV=cn ECC_for_Trae-v20260425/.trae/install.sh
> ```
>
> 其它安装步骤与.trae安装步骤一致。

这样在用户账号下开发的项目，皆可使用commant、Agent、skill和RULES工作流。

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

| 命令              | 用途           |
| ----------------- | -------------- |
| `/plan`           | 创建实施计划   |
| `/tdd`            | 测试驱动开发   |
| `/code-review`    | 质量审查       |
| `/build-fix`      | 修复构建错误   |
| `/e2e`            | 生成端到端测试 |
| `/verify`         | 运行验证循环   |
| `/refactor-clean` | 移除死代码     |
| `/learn`          | 提取模式       |

### 智能体

智能体是具有特定工具配置的专门 AI 助手。所有智能体都直接复用自项目根目录的 `agents/` 文件夹。

| 智能体                | 用途            | 使用场景         |
| --------------------- | --------------- | ---------------- |
| `planner`             | 实施规划        | 复杂功能         |
| `architect`           | 系统设计        | 架构决策         |
| `tdd-guide`           | 测试驱动开发    | 新功能、错误修复 |
| `code-reviewer`       | 质量审查        | 编写代码后       |
| `security-reviewer`   | 安全审计        | 提交前           |
| `go-reviewer`         | Go 代码审查     | Go 项目          |
| `python-reviewer`     | Python 代码审查 | Python 项目      |
| `rust-reviewer`       | Rust 代码审查   | Rust 项目        |
| `typescript-reviewer` | TS/JS 审查      | TypeScript 项目  |

### 技能

技能是通过聊天中的 `/` 菜单调用的按需工作流。所有技能都直接复用自项目的 `skills/` 文件夹。

| 技能               | 用途                  |
| ------------------ | --------------------- |
| `tdd-workflow`     | TDD 方法论            |
| `security-review`  | 安全检查清单          |
| `coding-standards` | 编码最佳实践          |
| `api-design`       | REST API 模式         |
| `e2e-testing`      | Playwright 端到端测试 |
| `eval-harness`     | 评估框架              |

### 规则

规则提供始终适用的规则和上下文，塑造智能体处理代码的方式。所有规则都直接复用自项目根目录的 `rules/` 文件夹。

| 类别     | 文件                                                         |
| -------- | ------------------------------------------------------------ |
| 通用     | coding-style, git-workflow, testing, performance, patterns, hooks, agents, security |
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

#### 1. 开发代码流程示例

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
