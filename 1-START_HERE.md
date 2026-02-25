---
type: prompt
title: PRD Planning Prompt (Step 1 of 3)
version: 1.0.0
status: active
audience: coding-agent
summary: 'Step 1 of 3-step benchmarking workflow: agent reads complete PRD suite and produces a comprehensive implementation plan'
keywords:
  - prd
  - planning
  - benchmarking
  - agent-evaluation
tags:
  - prompt
  - workflow
  - step-1
  - planning
created: '2026-02-25'
updated: '2026-02-25'
---

# START HERE

You are being given a complete product specification to build. The `docs/prd/` folder contains everything required to understand and implement a fully functional application.

**Your task:** Read and deeply understand all documentation in `docs/prd/`, then create a comprehensive implementation plan and build the system.

---

## Documents

### Core Requirements

Read these first, in order:

1. **`docs/prd/showbiz_prd.md`** — The primary product requirements document. Defines what the app does.

2. **`docs/prd/showbiz_infra_rider_prd.md`** — Infrastructure and execution requirements. Defines how builds must run.

### Supporting Documents

All documents in `docs/prd/supporting_docs/` provide critical detail referenced by the main PRD. Read all of them, including:

- `ai_prompting_context.md` — AI behavioral contracts
- `ai_voice_personality.md` — AI persona and voice specification
- `concept_system.md` — Concept-based taste discovery system
- `detail_page_experience.md` — Show detail page UX specification
- `discovery_quality_bar.md` — Quality acceptance criteria for AI discovery
- `technical_docs/storage-schema.md` — Data persistence and schema specification
- `technical_docs/storage-schema.ts` — TypeScript type definitions (reference only)

### Architecture Reference

- `docs/prd/supporting_docs/frontend-architecture.md` — Frontend coding standards and fractal architecture pattern

---

## Expectations

- **Read everything.** Do not start planning until you have read every document in `docs/prd/`.

- **Understand the relationships.** These documents reference and depend on each other. A surface-level read will miss important constraints.

- **Plan comprehensively.** Your implementation plan should demonstrate that you understood the full scope of what needs to be built and how it fits together.

- **Build completely.** Implement the system as specified.

---

## Expected Output

Your plan should include at minimum:

- **Architecture overview** — High-level system design and technology choices
- **Feature breakdown** — Each major feature area with implementation approach
- **Data model** — How the storage schema maps to implementation
- **AI integration** — How each AI surface (Ask, Alchemy, Explore Similar, Scoop) is implemented
- **Infrastructure** — How the infra rider constraints are satisfied
- **Testing strategy** — How critical functionality will be verified
- **Implementation order** — Sequencing that respects dependencies

---

## Begin

Read `docs/prd/showbiz_prd.md` now.

Write your implementation plan in a file called `results/PLAN.md`.