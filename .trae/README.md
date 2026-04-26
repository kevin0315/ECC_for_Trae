# Everything Claude Code for Trae

Bring Everything Claude Code (ECC) workflows to Trae IDE. This repository provides custom commands, agents, skills, and rules that can be installed into any Trae project with a single command.

## Quick Start

### Option 1: Local Installation (Current Project Only)

```bash
# Install to current project
cd /path/to/your/project
TRAE_ENV=cn .trae/install.sh
```

This creates `.trae-cn/` in your project directory.

### Option 2: Global Installation (All Projects)

```bash
# Install globally to ~/.trae-cn/
cd /path/to/your/project
TRAE_ENV=cn .trae/install.sh ~

# Or from the .trae folder directly
cd /path/to/your/project/.trae
TRAE_ENV=cn ./install.sh ~
```

This creates `~/.trae-cn/` which applies to all Trae projects.

### Option 3: Quick Install to Current Directory

```bash
# If already in project directory with .trae folder
cd .trae
./install.sh
```

The installer uses non-destructive copy - it will not overwrite your existing files.

## Installation Modes

### Local Installation

Install to the current project's `.trae` directory:

```bash
cd /path/to/your/project
TRAE_ENV=cn .trae/install.sh
```

This creates `/path/to/your/project/.trae-cn/` with all ECC components.

### Global Installation

Install to your home directory's `.trae-cn` directory (applies to all Trae projects):

```bash
# From project directory
TRAE_ENV=cn .trae/install.sh ~

# Or directly from .trae folder
cd .trae
TRAE_ENV=cn ./install.sh ~
```

This creates `~/.trae-cn/` with all ECC components. All Trae projects will use these global installations.

**Note**: Global installation is useful when you want to maintain a single copy of ECC across all your projects.

## Environment Support

- **Default**: Uses `.trae` directory
- **CN Environment**: Uses `.trae-cn` directory (set via `TRAE_ENV=cn`)

### Force Environment

```bash
# From project root, force the CN environment
TRAE_ENV=cn .trae/install.sh

# From inside the .trae folder
cd .trae
TRAE_ENV=cn ./install.sh
```

**Note**: `TRAE_ENV` is a global environment variable that applies to the entire installation session.

## Uninstall

The uninstaller uses a manifest file (`.ecc-manifest`) to track installed files, ensuring safe removal:

```bash
# Uninstall from current directory (if already inside .trae or .trae-cn)
cd .trae-cn
./uninstall.sh

# Or uninstall from project root
cd /path/to/your/project
TRAE_ENV=cn .trae/uninstall.sh

# Uninstall globally from home directory
TRAE_ENV=cn .trae/uninstall.sh ~

# Will ask for confirmation before uninstalling
```

### Uninstall Behavior

- **Safe removal**: Only removes files tracked in the manifest (installed by ECC)
- **User files preserved**: Any files you added manually are kept
- **Non-empty directories**: Directories containing user-added files are skipped
- **Manifest-based**: Requires `.ecc-manifest` file (created during install)

### Environment Support

Uninstall respects the same `TRAE_ENV` environment variable as install:

```bash
# Uninstall from .trae-cn (CN environment)
TRAE_ENV=cn ./uninstall.sh

# Uninstall from .trae (default environment)
./uninstall.sh
```

**Note**: If no manifest file is found (old installation), the uninstaller will ask whether to remove the entire directory.

## What's Included

### Context Files

- **TRAE.md** — Main Trae context file providing workflow guidance, coding standards, and security checklists
- **AGENTS.md** — Trae-specific agent instructions and model recommendations

### Commands

Commands are on-demand workflows invocable via the `/` menu in Trae chat. All commands are reused directly from the project root's `commands/` folder.

| Command | Purpose |
|---------|---------|
| `/plan` | Create implementation plan |
| `/tdd` | Test-driven development |
| `/code-review` | Quality review |
| `/build-fix` | Fix build errors |
| `/e2e` | Generate E2E tests |
| `/verify` | Run verification loop |
| `/refactor-clean` | Remove dead code |
| `/learn` | Extract patterns |

### Agents

Agents are specialized AI assistants with specific tool configurations. All agents are reused directly from the project root's `agents/` folder.

| Agent | Purpose | When to Use |
|-------|---------|-------------|
| `planner` | Implementation planning | Complex features |
| `architect` | System design | Architectural decisions |
| `tdd-guide` | Test-driven development | New features, bug fixes |
| `code-reviewer` | Quality review | After writing code |
| `security-reviewer` | Security audit | Before commits |
| `go-reviewer` | Go code review | Go projects |
| `python-reviewer` | Python code review | Python projects |
| `rust-reviewer` | Rust code review | Rust projects |
| `typescript-reviewer` | TS/JS review | TypeScript projects |

### Skills

Skills are on-demand workflows invocable via the `/` menu in chat. All skills are reused directly from the project's `skills/` folder.

| Skill | Purpose |
|-------|---------|
| `tdd-workflow` | TDD methodology |
| `security-review` | Security checklist |
| `coding-standards` | Coding best practices |
| `api-design` | REST API patterns |
| `e2e-testing` | Playwright E2E |
| `eval-harness` | Evaluation framework |

### Rules

Rules provide always-on rules and context that shape how the agent works with your code. All rules are reused directly from the project root's `rules/` folder.

| Category | Files |
|----------|-------|
| Common | coding-style, git-workflow, testing, performance, patterns, hooks, agents, security |
| Language-specific | typescript, python, golang, swift, php, java, kotlin, rust, cpp, csharp, dart, perl |

## Usage

1. Type `/` in chat to open the commands menu
2. Select a command or skill
3. The agent will guide you through the workflow with specific instructions and checklists

## Project Structure

```
.trae/ (or .trae-cn/)
├── TRAE.md           # Trae context file (workflow guidance)
├── AGENTS.md        # Trae agent supplement
├── commands/        # 72 command files (reused from project root)
├── agents/          # 38 agent files (reused from project root)
├── skills/          # Skill directories (reused from skills/)
├── rules/           # Rule files (reused from project root)
├── install.sh       # Install script
├── uninstall.sh     # Uninstall script
└── README.md        # This file
```

## How It Works

### Context Loading

When Trae starts a session in a project with ECC installed:

1. **TRAE.md** is loaded — provides Trae-specific workflow guidance
2. **AGENTS.md** is loaded — provides agent instructions and model recommendations
3. **Rules** from `rules/` are loaded — provide always-follow guidelines

### Command Execution

When you invoke a command via `/`:

1. Trae reads the command file from `.trae/commands/`
2. The command provides workflow instructions
3. The agent executes the workflow with specific steps

### Agent Delegation

For complex tasks, agents are used:

1. Task is analyzed and assigned to appropriate agent
2. Agent uses its specialized tools and knowledge
3. Results are synthesized back to the main session

## Customization

All files are yours to modify after installation. The installer never overwrites existing files, so your customizations are safe across re-installs.

**Note**: The `install.sh` and `uninstall.sh` scripts are automatically copied to the target directory during installation, so you can run these commands directly from your project.

## Recommended Workflow

1. **Start with planning**: Use `/plan` command to break down complex features
2. **Write tests first**: Invoke `/tdd` command before implementing
3. **Review your code**: Use `/code-review` after writing code
4. **Check security**: Use `/code-review` again for auth, API endpoints, or sensitive data handling
5. **Fix build errors**: Use `/build-fix` if there are build errors
6. **Verify before commit**: Use `/verify` to run verification loop

## Coding Standards

- **Immutability** - Always create new objects, never mutate existing ones
- **Small functions** - Functions under 50 lines, files under 800 lines
- **Input validation** - Validate at system boundaries
- **Error handling** - Fail loudly with clear messages
- **No hardcoded secrets** - Use environment variables

## Security Checklist

Before any commit:

- No hardcoded API keys, passwords, or tokens
- All external input validated
- Parameterized queries for database writes
- Sanitized HTML output where applicable
- Authz/authn checked for sensitive paths

## Testing Requirements

- **Minimum coverage: 80%**
- Unit tests for individual functions
- Integration tests for API endpoints
- E2E tests for critical user flows

## Next Steps

- Open your project in Trae
- Type `/` to see available commands
- Enjoy the ECC workflows!
