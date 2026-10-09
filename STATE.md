# SDD skill-pack — session state

Last updated: 2026-09-11.

## What this repo is
Reusable spec-driven-development skill-pack: `CLAUDE.md` + `.claude/skills/sdd-*` meant to be copied into a target project repo (not a product built here). Research backing this lives in `00-index.md` through `07-allegro-tech-best-practices.md`.

## Status: pipeline v1 built, unreviewed by human, not yet dry-run on a real feature.

## Built
- `CLAUDE.md` — pipeline overview, repo layout (`memory/constitution.md`, `specs/<slug>/{spec,plan,tasks,notes}.md`), context-management rules, do/don't.
- `.claude/skills/sdd-constitution/SKILL.md` — one-time interview → `memory/constitution.md`.
- `.claude/skills/sdd-specify/SKILL.md` → `spec.md` (EARS + Given/When/Then, `[NEEDS CLARIFICATION]` markers).
- `.claude/skills/sdd-plan/SKILL.md` → `plan.md` (HOW, traces to spec, constitution-compliance check).
- `.claude/skills/sdd-tasks/SKILL.md` → `tasks.md` (context-sized, `[P]`-flagged, acceptance criteria carried forward).
- `.claude/skills/sdd-implement/SKILL.md` — one task/wave at a time, TDD, fresh session recommended per task.
- `.claude/skills/sdd-validate/SKILL.md` — re-checks acceptance criteria fresh, logs drift to `notes.md`, never silently edits spec.

Every skill hard-stops after writing its artifact; none auto-chains to the next.

## Design decisions made (with rationale)
- Added a validate phase — not in Spec Kit/Kiro, pulled from Allegro + Thoughtworks' "re-iterate spec after implementation."
- No skip-gate fast path (Kiro's Quick Spec) — user wants every step human-checked, no exceptions.
- No wave scheduler — `[P]` flag only, concurrent execution left to the human.
- Constitution is a freeform interview grounded in the actual repo, not Spec Kit's fixed 9-article template.
- Code stays the persisted artifact (Spec Kit/Kiro hybrid), not Tessl's fully-regenerable-from-spec model — Thoughtworks' determinism objection was the reason.
- No clause-ID↔test traceability (Sean Grove's Model Spec pattern) — acceptance criteria flow spec→tasks→tests but without stable IDs.
- Context-management rules (file-as-state not conversation, per-feature isolation, fresh session per task) are original additions, not sourced from any reviewed tool.

## Known gaps / deliberately not built
- No git branch/issue automation (Spec Kit auto-branches, `taskstoissues`).
- No Design-First workflow variant (Kiro: start from architecture, derive requirements after).
- No spec-quality scoring (Thoughtworks: industry has no consensus metric here).

## Next steps (pick up here)
1. Human review of the 6 SKILL.md files + CLAUDE.md themselves.
2. Dry-run the full chain on one real vague requirement end-to-end; check task sizing (≤3 files) and gate-stop behavior actually hold up in practice.
3. Decide whether to add: clause-ID traceability, a wave scheduler, a Design-First variant, or a packaged Spec Kit-style article template for `sdd-constitution`.
4. Decide install mechanism for target repos: plain copy vs. Claude Code plugin packaging.
