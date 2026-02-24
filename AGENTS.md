# AGENTS.md

## Project Overview

- Project: `deep-dive-research-skill`
- Primary runtime(s): Claude Code agents (Explore, general-purpose)
- Main entrypoint(s): `SKILL.md`, `.claude/agents/research-orchestrator.md`

## Harness Commands

Run from repository root:

| Goal | Command |
|---|---|
| Fast sanity check | `make smoke` |
| Static quality gates | `make check` |
| Full verification | `make test` |
| Research audit | `make research-audit` |
| Governance audit | `make control-audit` |

## Agent Roster

| Agent | Model | Role | Skills |
|---|---|---|---|
| `research-orchestrator` | opus | Coordinates full research workflow | all |
| `financial-researcher` | sonnet | Financial and funding analysis | financial-deep-research |
| `competitive-analyst` | sonnet | Competitive landscape and positioning | competitor-intel |
| `market-product-analyst` | sonnet | Product metrics and market opportunity | app-store-optimization |
| `governance-auditor` | haiku | Quality and compliance validation | agent-control-metalayer-skill |

## Constraints and Guardrails

- Prefer deterministic scripts over interactive/manual steps.
- Keep command names stable (`smoke`, `check`, `test`, `research-audit`, `control-audit`).
- Update docs and scripts in the same change when workflow behavior changes.
- Avoid side effects outside the research output folder.
- Never bypass `check` or `test` without explicit escalation.
- Do not merge changes without corresponding documentation updates.
- Escalate to human when retry budget is exhausted.

## Architecture Boundaries

- Parse and validate research inputs at boundaries (user request parsing).
- Keep internal data models typed and normalized (research dimensions, metrics).
- Keep each agent focused on one responsibility.
- Document boundary ownership below.

### Boundary Map

| Boundary | Input | Output | Owner |
|---|---|---|---|
| Request Parsing | User prompt | Research charter | research-orchestrator |
| Financial Research | Research charter | Financial analysis report | financial-researcher |
| Competitive Research | Research charter | Competitive analysis report | competitive-analyst |
| Market/Product Research | Research charter | Market/product analysis report | market-product-analyst |
| Synthesis | Agent reports | Executive summary + deep-dives | research-orchestrator |
| Quality Audit | Final reports | Audit report with pass/fail | governance-auditor |

## Observability Expectations

- Include `trace_id` and `run_id` in long-running workflow logs.
- Emit structured event names for major transitions (start, step, success, failure).
- Keep event fields stable for querying and alerting.
- Document source count, confidence levels, and data freshness per report.

### Required Events

| Event | When | Fields |
|---|---|---|
| `research.start` | Research initiated | subject, scope, focus_areas |
| `research.agent.deploy` | Specialist agent launched | agent_name, research_dimensions |
| `research.agent.complete` | Specialist agent finished | agent_name, source_count, word_count |
| `research.synthesis.start` | Synthesis phase begins | agent_count, total_sources |
| `research.audit.result` | Governance audit complete | pass_fail, quality_score, issues |
| `research.complete` | All reports delivered | total_words, total_sources, total_files |

## Execution Plans

- For tasks expected to exceed ~30 minutes, create/update `PLANS.md` before coding.
- Track scope, constraints, milestones, and verification steps.
- Update status checkpoints during execution and after major decisions.

## Static Analysis and Quality Gates

- Run `make check` before `make test`.
- Run source verification before publishing reports.
- Treat missing citations as blocking.

## Entropy Management

- Remove stale research templates and outdated examples.
- Keep agent definitions and skill dependencies in sync.
- Run periodic audits to ensure documentation matches behavior.

## Control Policy

### Gate Sequence

1. `smoke` - Verify agent definitions and skill dependencies exist
2. `check` - Validate SKILL.md frontmatter, agent YAML, source formatting
3. `test` - Run sample research workflow and verify output structure
4. `research-audit` - Validate research outputs against quality standards
5. `control-audit` - Full governance and compliance check

### Retry Budget

- Per-agent research: 2 retries before escalation
- Source verification: 3 retries per source
- Full workflow: 1 retry before human escalation

### Escalation Conditions

- Agent fails after retry budget exhausted
- Source count below minimum threshold (3 per claim)
- Contradictory data across agents without resolution
- Quality score below 7/10 on governance audit
