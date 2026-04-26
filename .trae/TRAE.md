# ECC for Trae IDE

This file provides Trae IDE with the baseline ECC workflow, review standards, and security checks for repositories that install the Trae target.

## Overview

Everything Claude Code (ECC) is a cross-harness coding system with 38 specialized agents, 156 skills, and 72 commands. This Trae-specific configuration supplements the root `AGENTS.md` with Trae-specific guidance and ensures full compatibility with Trae IDE's plugin system.

## Core Workflow

1. **Plan before editing** - Use `/plan` command for complex features
2. **Test-first changes** - Prefer TDD for bug fixes and new functionality using `/tdd`
3. **Review for security** - Use `/code-review` before shipping
4. **Keep changes self-contained** - Readable and easy to revert
5. **Verify before commit** - Run verification loops with `/verify`

## Available Commands

All ECC commands are available via the `/` menu in Trae chat:

| Command | Purpose |
|---------|---------|
| `/plan` | Create implementation plan |
| `/tdd` | Test-driven development workflow |
| `/code-review` | Quality and security review |
| `/build-fix` | Fix build errors |
| `/e2e` | Generate end-to-end tests |
| `/refactor-clean` | Remove dead code |
| `/verify` | Run verification loop |
| `/eval` | Evaluate against criteria |
| `/test-coverage` | Analyze test coverage |
| `/update-docs` | Update documentation |
| `/learn` | Extract patterns from session |

## Available Agents

ECC provides 38 specialized agents. Use these for complex tasks:

| Agent | Purpose | When to Use |
|-------|---------|-------------|
| `planner` | Implementation planning | Complex features, refactoring |
| `architect` | System design | Architectural decisions |
| `tdd-guide` | Test-driven development | New features, bug fixes |
| `code-reviewer` | Quality review | After writing code |
| `security-reviewer` | Vulnerability detection | Before commits |
| `e2e-runner` | E2E testing | Critical user flows |
| `go-reviewer` | Go code review | Go projects |
| `python-reviewer` | Python code review | Python projects |
| `rust-reviewer` | Rust code review | Rust projects |
| `typescript-reviewer` | TS/JS review | TypeScript projects |

## Coding Standards

- **Immutability** - Always create new objects, never mutate existing ones
- **Small functions** - Keep functions under 50 lines
- **Focused files** - Files should be under 800 lines
- **Input validation** - Validate at system boundaries
- **No hardcoded secrets** - Use environment variables
- **Error handling** - Fail loudly with clear messages

## Security Checklist

Before any commit:

- No hardcoded API keys, passwords, or tokens
- All external input validated
- Parameterized queries for database writes
- Sanitized HTML output where applicable
- Authz/authn checked for sensitive paths
- Error messages scrubbed of sensitive internals

## Delivery Standards

- Use conventional commits: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`, `ci`
- Run targeted verification for touched areas before shipping
- Prefer contained local implementations over adding new third-party runtime dependencies
- Maintain 80%+ test coverage

## TDD Workflow

1. **Write failing test (RED)** - Test should fail before implementation
2. **Minimal implementation (GREEN)** - Write just enough code to pass
3. **Refactor (IMPROVE)** - Clean up while maintaining functionality
4. **Verify 80%+ coverage** - Ensure adequate test coverage

## Key Differences from Claude Code

| Feature | Claude Code | Trae |
|---------|------------|------|
| Context file | CLAUDE.md + AGENTS.md | AGENTS.md + TRAE.md |
| Hooks | Full hook system | Hook-based via rules |
| Commands | `/slash` commands | `/slash` commands |
| Agents | 38 agents | 38 agents (shared) |
| Skills | Via plugin | Via rules installation |

## Installation

After installing ECC for Trae:

1. Commands appear via `/` menu
2. Agents are loaded from `.trae/agents/`
3. Skills are loaded from `.trae/skills/`
4. Rules are loaded from `.trae/rules/`

## Project Structure

```
.trae/
├── TRAE.md           # This file - Trae-specific context
├── AGENTS.md         # Trae-specific agent supplement
├── commands/         # 72 slash commands
├── agents/           # 38 specialized agents
├── skills/           # 156 workflow skills
├── rules/            # Always-follow guidelines
├── install.sh        # Installation script
└── uninstall.sh      # Uninstallation script
```

## Using Skills

Skills are the canonical workflow surface. Invoke via `/` menu:

- `tdd-workflow` - Test-driven development
- `security-review` - Comprehensive security checklist
- `coding-standards` - Universal coding standards
- `api-design` - REST API design patterns
- `e2e-testing` - Playwright E2E patterns

## ECC Areas To Reuse

- `AGENTS.md` for repo-wide operating rules
- `skills/` for deep workflow guidance
- `commands/` for slash-command patterns
- `mcp-configs/` for shared connector baselines
- `rules/` for always-follow guidelines
