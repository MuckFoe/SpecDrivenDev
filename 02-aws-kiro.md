# AWS Kiro (Spec-Driven Agentic IDE)

**Source:** Kiro docs, "Feature Specs"
**URL:** https://kiro.dev/docs/specs/feature-specs/
**Type:** Commercial AI IDE from AWS.

## Core Claim
Requirements, design, and tasks are written into the repo *before* coding starts; the agent then works the resulting list, in parallel where possible.

## Artifacts (written to repo)
- `requirements.md` (or `bugfix.md`) — user stories + acceptance criteria in **EARS notation** (WHEN/THEN).
- `design.md` — technical architecture, sequence diagrams, implementation considerations.
- `tasks.md` — discrete, trackable tasks/sub-tasks, each with inputs, outputs, dependencies.

## Workflow variants
- **Requirements-First:** Requirements → Design → Tasks (default; start from desired behavior).
- **Design-First:** Design → Requirements → Tasks (start from an architecture/low-level design, derive requirements after).
- **Quick Spec:** runs all three phases automatically, **skipping approval gates** — a deliberate speed/rigor tradeoff, not the default.

## Execution model
Tasks are grouped into **waves**: tasks within a wave run concurrently; waves run sequentially. This is the mechanism for controlled parallelism without losing dependency ordering.

## Do
- Use Feature Specs for complex, multi-task features and anything needing team-shared documentation.
- Pick the workflow variant (Requirements-First vs Design-First) to match your actual starting point rather than forcing one.
- Keep the approval gates between phases for anything non-trivial (review requirements, then design, then tasks).
- Give each task explicit inputs, outputs, and dependencies so waves can parallelize safely.

## Don't
- Don't use Feature Specs for simple bug fixes — Kiro has a separate lighter Bugfix Spec path for that.
- Don't start a spec without clarity on either requirements or design direction — that's what the Analyze Requirements phase is for; don't skip it when requirements need validation.
- Don't reach for Quick Spec (no approval gates) for anything you haven't already de-risked — it trades review checkpoints for speed.
- Don't use for pure exploratory coding with no clear goal — spec overhead isn't justified there.
