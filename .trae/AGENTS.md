# ECC for Trae — Agent Instructions

This supplements the root `AGENTS.md` with Trae-specific guidance.

## Model Recommendations

| Task Type | Recommended Model |
|-----------|------------------|
| Routine coding, tests, formatting | Default (Sonnet) |
| Complex features, architecture | Opus or equivalent |
| Debugging, refactoring | Sonnet |
| Security review | Opus or equivalent |

## Skills Discovery

Skills are loaded from the `.trae/skills/` directory. Each skill contains:
- `SKILL.md` — Detailed instructions and workflow
- Workflow guidance for specialized tasks

Available skills:
- `tdd-workflow` — Test-driven development with 80%+ coverage
- `security-review` — Comprehensive security checklist
- `coding-standards` — Universal coding standards
- `frontend-patterns` — React/Next.js patterns
- `backend-patterns` — API design, database, caching
- `e2e-testing` — Playwright E2E tests
- `eval-harness` — Eval-driven development
- `api-design` — REST API design patterns
- `verification-loop` — Build, test, lint, typecheck, security
- `deep-research` — Multi-source research

## Key Differences from Claude Code

| Feature | Claude Code | Trae |
|---------|------------|------|
| Context file | CLAUDE.md + AGENTS.md | AGENTS.md + TRAE.md |
| Hook system | Full hook events | Rule-based hooks |
| Package manager | Auto-detected | Auto-detected |
| MCP servers | Via settings.json | Via Trae config |
| Agent delegation | Built-in Task tool | Via skills/agents |

## Security Enforcement

Since Trae uses rule-based enforcement:
1. Always validate inputs at system boundaries
2. Never hardcode secrets — use environment variables
3. Review `git diff` before every push
4. Run security checks before committing
5. Use verification loops to ensure code quality

## Workflow Integration

Trae workflows integrate with ECC via:

1. **Commands** — Available via `/` menu
2. **Agents** — Loaded from `.trae/agents/`
3. **Skills** — Loaded from `.trae/skills/`
4. **Rules** — Loaded from `.trae/rules/`

## Agent Orchestration

Use agents proactively without user prompt:
- Complex feature requests → **planner**
- Code just written/modified → **code-reviewer**
- Bug fix or new feature → **tdd-guide**
- Architectural decision → **architect**
- Security-sensitive code → **security-reviewer**

Use parallel execution for independent operations — launch multiple agents simultaneously.

## Testing Requirements

**Minimum coverage: 80%**

Test types (all required):
1. **Unit tests** — Individual functions, utilities, components
2. **Integration tests** — API endpoints, database operations
3. **E2E tests** — Critical user flows

**TDD workflow:**
1. Write test first (RED) — test should FAIL
2. Write minimal implementation (GREEN) — test should PASS
3. Refactor (IMPROVE) — verify coverage 80%+

## Git Workflow

**Commit format:** `<type>: <description>` — Types: feat, fix, refactor, docs, test, chore, perf, ci

**PR workflow:** Analyze full commit history → draft comprehensive summary → include test plan → push with `-u` flag.
