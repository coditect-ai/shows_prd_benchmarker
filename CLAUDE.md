---
type: documentation
title: PRD Benchmarker - AI Agent Context
version: 1.0.0
status: active
scope: shows-prd-benchmarker tool
audience: ai-agent
created: '2026-02-25'
updated: '2026-02-25'
---

# PRD Benchmarker - AI Agent Context

Core framework directives are in the parent `.claude/CLAUDE.md` (loaded automatically).
This file provides tool-specific guidance for the PRD benchmarking workflow.

---

## Critical Rules

1. **Fresh context per step.** Steps 1, 2, and 3 MUST each run in a separate conversation. Never evaluate a plan in the same context that produced it.

2. **Read everything before acting.** In Steps 1 and 2, read ALL files in `docs/prd/` including every file in `supporting_docs/` before producing any output. Surface-level reads miss critical constraints.

3. **Anchor every requirement.** In Step 2, every extracted requirement MUST cite a specific PRD file and section heading. If you cannot cite it, delete it.

4. **Be honest about coverage.** If a plan only implies or vaguely references a requirement, score it `partial`, not `full`. Absence = `missing`.

5. **Interpret, don't restate.** The coverage narrative must synthesize patterns ("gaps cluster around AI behavioral contracts") not echo table data ("6 items are partial").

---

## Workflow

| Step | Prompt File | Output | Fresh Context? |
|------|-------------|--------|----------------|
| 1 | `1-START_HERE.md` | `results/PLAN.md` | Yes |
| 2 | `2-EVALUATE_PLAN.md` | `results/PLAN_EVAL.md` | Yes (new conversation) |
| 3 | `3-PLAN_EVAL_REPORT.md` | `results/PLAN_EVAL_REPORT.html` | Yes (new conversation) |

---

## PRD Reading Order

1. `docs/prd/showbiz_prd.md` (primary specification)
2. `docs/prd/showbiz_infra_rider_prd.md` (infrastructure constraints)
3. All files in `docs/prd/supporting_docs/` (detailed specifications)
4. `docs/prd/supporting_docs/technical_docs/` (data schemas)

---

## Exact Labels (No Variants)

**Coverage:** `full` | `partial` | `missing`
**Severity:** `critical` | `important` | `detail`

---

## Frontend Architecture Reference

The ShowBiz PRD assumes a fractal frontend architecture. See `docs/prd/supporting_docs/frontend-architecture.md` for the coding standards the benchmarked plan should address.

---

**CODITECT Integration:** `skills/prd-benchmarker/SKILL.md` | `commands/prd-benchmark.md` | `agents/prd-benchmarker-specialist.md`
