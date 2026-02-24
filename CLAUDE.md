# CLAUDE.md

## Project

Deep-Dive Research Orchestrator - a Claude Code skill for comprehensive multi-dimensional research using coordinated AI specialist agents.

## Key Files

- [SKILL.md](SKILL.md) - Skill specification and frontmatter
- [AGENTS.md](AGENTS.md) - Agent roster, harness commands, constraints, and governance
- [METHODOLOGY.md](METHODOLOGY.md) - Research workflow and methodology
- [PLANS.md](PLANS.md) - Execution plans for multi-step work
- [.claude/agents/](/.claude/agents/) - Agent definitions

## Agents

Five agents defined in `.claude/agents/`:

| Agent | File | Model | Purpose |
|---|---|---|---|
| research-orchestrator | `.claude/agents/research-orchestrator.md` | opus | Coordinates all agents and synthesizes reports |
| financial-researcher | `.claude/agents/financial-researcher.md` | sonnet | Financial and funding analysis |
| competitive-analyst | `.claude/agents/competitive-analyst.md` | sonnet | Competitive landscape and positioning |
| market-product-analyst | `.claude/agents/market-product-analyst.md` | sonnet | Product metrics and market opportunity |
| governance-auditor | `.claude/agents/governance-auditor.md` | haiku | Quality and compliance validation |

## Commands

```bash
make smoke          # Verify agents and dependencies exist
make check          # Validate frontmatter and YAML
make test           # Run sample research workflow
make research-audit # Validate research outputs
make control-audit  # Full governance check
```

## Rules

- Every major claim requires 3+ independent sources with URLs
- All metrics must include source attribution and dates
- Information gaps must be explicitly documented
- Estimates must be clearly marked as estimates
- Never bypass quality gates without escalation
- Update AGENTS.md and PLANS.md when workflow behavior changes
- Keep agent definitions in sync with SKILL.md dependencies

## Dependencies

### Required
- `financial-deep-research` - Financial analysis
- `competitor-intel` - Competitive intelligence
- `app-store-optimization` - Product and market metrics

### Optional
- `agent-control-metalayer-skill` - Governance framework
- `harness-engineering-skill` - Deterministic workflows
