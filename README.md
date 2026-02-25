---
type: tool
component_type: tool
title: PRD Coverage Benchmarker
name: shows-prd-benchmarker
version: 1.0.0
status: active
audience: contributor
summary: 'Benchmark AI agent planning quality against product specifications using a 3-step evaluation workflow: plan, evaluate coverage, generate stakeholder report'
keywords:
  - prd
  - benchmark
  - evaluation
  - coverage
  - planning
  - agent-quality
  - stakeholder-report
tags:
  - tool
  - evaluation
  - benchmarking
  - qa
created: '2026-02-25'
updated: '2026-02-25'
track: H
cef_track: H-19
origin: bladnman/shows_prd_benchmarker
fork: coditect-ai/shows_prd_benchmarker
---

# PRD Coverage Benchmarker

Benchmark how well AI coding agents plan against a real product specification. Feed it a PRD, get an implementation plan, evaluate coverage, and generate a stakeholder-ready HTML report.

## Features

- **3-Step Evaluation Workflow** — Plan generation, coverage audit, and visual report as independent phases
- **Fresh Context Isolation** — Each step runs in a separate conversation to prevent evaluator bias
- **Rigorous Requirements Extraction** — Two-pass methodology: identify functional areas, then extract anchored requirements
- **Severity-Tiered Coverage Scoring** — Critical/important/detail classification with weighted scoring formula
- **Stakeholder-Ready HTML Dashboard** — Self-contained visual report for 60-second executive comprehension
- **Sample PRD Included** — Complex multi-document ShowBiz specification for regression benchmarking
- **Evidence-Based Evaluation** — Every coverage rating requires plan citation; every requirement requires PRD anchor

## Architecture

```
Step 1: PLAN            Step 2: EVALUATE          Step 3: REPORT
┌───────────────┐      ┌───────────────────┐     ┌───────────────────┐
│ Agent reads    │      │ Fresh agent reads  │     │ Fresh agent reads  │
│ full PRD suite │─────▶│ PRD + PLAN.md     │────▶│ PLAN_EVAL.md      │
│ Produces       │      │ Extracts reqs     │     │ Generates HTML     │
│ PLAN.md        │      │ Scores coverage   │     │ dashboard          │
└───────────────┘      │ Produces          │     │ PLAN_EVAL_REPORT   │
                       │ PLAN_EVAL.md      │     │ .html              │
                       └───────────────────┘     └───────────────────┘
```

**Key design decision:** Each step uses a fresh context (new conversation). This prevents the evaluator from being biased by having produced the plan, and prevents the report generator from being influenced by evaluation reasoning.

### Scoring Formula

```
coverage_score = (full_count x 1.0 + partial_count x 0.5) / total_count x 100
```

Scores are calculated overall and per severity tier (critical, important, detail).

## Setup

### Prerequisites

- An AI coding agent capable of reading multi-file documentation (Claude Code, Cursor, Windsurf, etc.)
- A PRD document set (or use the included ShowBiz sample)

### Installation

This tool is included as a submodule in the CODITECT platform:

```bash
# Already available at:
submodules/tools/shows-prd-benchmarker/
```

No dependencies to install — this is a pure prompt/document tool.

### CODITECT Integration

```bash
# Via slash command
/prd-benchmark full --sample

# Via skill
# Load skill: prd-benchmarker
# Load agent: prd-benchmarker-specialist
```

## Usage

### Quick Start (Using Sample PRD)

```bash
# Step 1: In a fresh conversation, tell your agent:
"Read 1-START_HERE.md and follow its instructions."
# Output: results/PLAN.md

# Step 2: In a NEW conversation:
"Read 2-EVALUATE_PLAN.md and follow its instructions."
# Output: results/PLAN_EVAL.md

# Step 3: In a NEW conversation:
"Read 3-PLAN_EVAL_REPORT.md and follow its instructions."
# Output: results/PLAN_EVAL_REPORT.html
```

### Using Your Own PRD

Replace the contents of `docs/prd/` with your own product specification documents. The workflow prompts reference this directory.

### Example Output

After running all 3 steps, you get:

| File | Description |
|------|-------------|
| `results/PLAN.md` | Comprehensive implementation plan |
| `results/PLAN_EVAL.md` | Coverage evaluation with scored requirements table |
| `results/PLAN_EVAL_REPORT.html` | Visual stakeholder dashboard |

### Interpreting Scores

| Score Range | Interpretation |
|-------------|----------------|
| 90-100% | Exceptional coverage — minor polish gaps only |
| 75-89% | Strong plan — some areas need more detail |
| 60-74% | Structural gaps — significant requirements missed |
| <60% | Fundamental coverage issues — major rework needed |

## Repository Structure

```
shows-prd-benchmarker/
├── README.md                    # This file
├── CLAUDE.md                    # Tool-specific AI guidance
├── 1-START_HERE.md              # Step 1: Planning prompt
├── 2-EVALUATE_PLAN.md           # Step 2: Evaluation prompt
├── 3-PLAN_EVAL_REPORT.md        # Step 3: Report generation prompt
├── docs/
│   ├── prd/                     # Sample PRD suite (ShowBiz)
│   │   ├── showbiz_prd.md       # Primary product specification
│   │   ├── showbiz_infra_rider_prd.md  # Infrastructure constraints
│   │   └── supporting_docs/     # 5 detailed spec documents + schema
│   └── extras/
│       └── plan_eval_prompt.md  # Alternative evaluation prompt (simpler)
└── results/                     # Output directory (gitignored)
```

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| Low coverage scores | Agent didn't read all PRD files | Verify agent read every file in `docs/prd/` including `supporting_docs/` |
| Inflated coverage | Evaluator biased by having produced plan | Use a FRESH context for each step |
| Missing requirements | Surface-level PRD reading | Ensure agent understands cross-document dependencies |
| HTML report is just a table | Report agent given no creative freedom | Re-run Step 3 emphasizing "stakeholder dashboard, not data dump" |
| Requirements not anchored | Evaluator inventing phantom requirements | Hard rule: every requirement must cite file + section |

## Related CODITECT Components

- **Skill:** `prd-benchmarker` — Full methodology reference
- **Command:** `/prd-benchmark` — Slash command interface
- **Agent:** `prd-benchmarker-specialist` — Specialized evaluation agent
- **Composable Skills:** `advanced-evaluation`, `evaluating-llm-outputs`, `qa-grading-framework`

## Origin

Forked from [bladnman/shows_prd_benchmarker](https://github.com/bladnman/shows_prd_benchmarker) to [coditect-ai/shows_prd_benchmarker](https://github.com/coditect-ai/shows_prd_benchmarker).

**License:** See upstream repository.
