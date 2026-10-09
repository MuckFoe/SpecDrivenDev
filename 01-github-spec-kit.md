# GitHub Spec Kit

**Source:** github/spec-kit repo, `spec-driven.md` methodology doc
**URL:** https://github.com/github/spec-kit/blob/main/spec-driven.md
**Type:** Open-source toolkit (MIT), released Sept 2025. Works with Copilot, Claude Code, Gemini CLI, 30+ agents.

## Core Claim
"Specifications don't serve code—code serves specifications." Specs are the primary artifact; code is a generated expression of them.

## Workflow (commands)
`/speckit.constitution` → `/speckit.specify` → `/speckit.plan` → `/speckit.tasks` → `/speckit.taskstoissues` → `/speckit.implement`

1. **constitution** — write project-level governing principles once.
2. **specify** — feature description → numbered feature branch + `specs/[branch]/spec.md` (requirements, acceptance criteria).
3. **plan** — spec → implementation plan; checks constitutional compliance; produces data models, API contracts, test scenarios, quickstart.
4. **tasks** — plan → `tasks.md`; independent tasks flagged `[P]` for parallel execution.
5. **implement** — execute tasks against approved tests.

## The 9 "Constitutional Articles" (governance template)
- I: every feature starts as a standalone library.
- II: libraries expose a CLI (text in / JSON out).
- III (Test-First Imperative): no implementation before tests are written, approved, and confirmed failing.
- IV–VI: project-defined (integration testing, observability, versioning).
- VII: max 3 projects for an initial implementation without documented justification.
- VIII: use framework features directly, don't wrap them.
- IX: integration-first testing — real DBs/services, not mocks.

## Do
- Mark every ambiguity with an explicit `[NEEDS CLARIFICATION]` marker instead of guessing.
- Keep specs at the WHAT/WHY level; keep plans high-level and readable.
- Write and get tests approved before writing implementation code.
- Test against real databases/services (integration-first).
- Link every technical choice back to a requirement.
- Treat spec consistency validation as continuous, not a one-time gate.

## Don't
- Don't put tech stack, APIs, or code structure into the feature spec — that belongs in the plan.
- Don't write implementation code before tests exist and are approved.
- Don't use mocks in place of real services for verification.
- Don't add speculative ("might need") features without a grounding user story.
- Don't exceed 3 initial projects, and don't wrap framework features unnecessarily.
- Don't let documentation and code diverge — SDD treats that drift as a defect, not an inevitability.

## Notable claim
Traditional requirements documentation ≈ 12 hours; SDD-command-driven spec authoring ≈ 15 minutes, with better ambiguity coverage.
