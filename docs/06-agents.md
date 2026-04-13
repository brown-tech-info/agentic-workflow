# Using Agents in this Repository

This repo provides specialized custom agents under `.github/agents/`.

## Recommended flow
1) Orchestrator: ensure Charter/Requirements/Plan are in place.
2) Requirements Analyst: tighten requirements + acceptance criteria.
3) Solution Architect: produce HLD/LLD and key tradeoffs.
4) Developer: implement the plan with minimal diffs.
5) Test Engineer: add tests and validation steps.
6) Security Reviewer: review changes and provide a Ship/No-Ship call.
7) Docs Editor: polish docs for public clarity.
8) Release Manager: generate PR/release notes.

## How agent selection works

- **Manual selection is deterministic.** Use `/agent` or `@agent-name` to invoke a specific agent. This always works and overrides any automatic routing.
- **Auto-routing is heuristic.** When `disable-model-invocation` is `false`, Copilot CLI *may* choose a specialist agent as a subagent when it determines a good fit based on the request. This is not guaranteed—it depends on Copilot's assessment of the task.
- **Restart required.** After adding, removing, or modifying files under `.github/agents/`, restart GitHub Copilot CLI to reload agent definitions.

### Auto-invocable agents (subagent-eligible)
| Agent | Trigger phrases |
|-------|----------------|
| requirements-analyst | requirements, acceptance criteria, scope |
| solution-architect | HLD, LLD, tradeoffs, threat model, trust boundaries |
| security-reviewer | security review, audit, secrets, PII/PHI |
| docs-editor | README, runbook, clarity, public polish |
| release-manager | PR description, release notes, checklists |
| test-engineer | tests, validation, verification, acceptance criteria coverage |

### Manual-only agents
| Agent | Reason |
|-------|--------|
| orchestrator | Phase gating requires explicit human intent. |
| developer | Implementation requires prior plan approval. |

## Role boundaries (important)
- security-reviewer is findings-only (no file edits).
- solution-architect and requirements-analyst are docs-only.
- developer is implementation-only and must follow plan + guardrails.
