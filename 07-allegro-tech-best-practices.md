# Allegro Tech — "Spec-Driven Development (SDD): Best Practices (So Far)"

**URL:** https://blog.allegro.tech/2026/06/spec-driven-development-best-practices.html
**Type:** Independent engineering-blog field report (practitioner synthesis, not a vendor).

## Workflow (4 phases)
1. **Specify** — gather requirements into product, technical, and integration specs.
2. **Plan** — decompose specs into self-contained tasks with acceptance criteria.
3. **Implement** — execute tasks separately via AI agents.
4. **Validate** — review code, run tests, update the spec based on what was learned.

## Do — Specification
- Write specs iteratively and collaboratively (PM + engineers + designers), not solo.
- Keep two separate documents: the **specification** (stable blueprint) vs. the **execution plan** (per-change delta) — don't conflate them.
- Include product description, users, functional/non-functional requirements, UI, and use cases.
- Extract shared technical requirements into an organization-wide reference file (don't repeat per-feature).
- Split into **per-feature specs** for medium/large projects — a monolithic spec degrades over time.
- Have an agent review the spec itself for clarity/completeness before using it.
- Calibrate detail to risk: high-criticality systems earn more spec detail; low-criticality systems don't.

## Don't — Specification
- Don't include implementation detail in the spec (blurs spec into code).
- Don't write specs solo.
- Don't over-specify (spec becomes pseudo-code) or under-specify (agent fills gaps with guesses) — both are named as symmetric failure modes.
- Don't skip re-iterating the spec after every implementation change — a spec that's only ever written once is already stale.

## Do — Implementation
- Break work into small, context-window-sized tasks.
- Write explicit acceptance criteria per task.
- Pair with TDD (tests double as acceptance criteria) and, for frontend, BDD (Given/When/Then).
- Scaffold a project template with dependencies pre-added for greenfield work.
- Run `/init`-equivalent to produce an `AGENTS.md` before planning starts.
- Evaluate output in a **fresh agent session** (a second agent reviews what the first missed).
- Do a thorough **human** review regardless — you own the production code, not the agent.

## Don't — Implementation
- Don't implement an entire feature spec in one shot — context-window limits make this unreliable.
- Don't let agent review substitute for human review.
- Don't apply SDD overhead to simple, low-complexity tasks.
