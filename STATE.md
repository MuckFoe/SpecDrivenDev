# SDD skill-pack — session state

Last updated: 2026-10-09.

## What this repo is
Reusable spec-driven-development skill-pack: `CLAUDE.md`, `.claude/skills/sdd-*` and `specs/` (index template, viewer, save server), meant to be copied into a target project repo (not a product built here). Research backing this lives in `00-index.md` through `07-allegro-tech-best-practices.md`.

## Status: pipeline v1 built and used on a first real project through specify → plan → tasks. Implement and validate have not been exercised yet. Skills unreviewed by human.

## Built
- `CLAUDE.md` — pipeline overview, repo layout (`memory/constitution.md`, `specs/README.md`, `specs/<slug>/{spec,plan,tasks,notes}.md`), viewer, context-management rules, do/don't.
- `.claude/skills/sdd-constitution/SKILL.md` — one-time interview → `memory/constitution.md`.
- `.claude/skills/sdd-specify/SKILL.md` → `spec.md` (EARS + Given/When/Then, `[NEEDS CLARIFICATION]` markers) and a row in `specs/README.md`.
- `.claude/skills/sdd-plan/SKILL.md` → `plan.md` (HOW, traces to spec, constitution-compliance check).
- `.claude/skills/sdd-tasks/SKILL.md` → `tasks.md` in a fixed format (waves table, checklist, one detail section per task), context-sized, `[P]`-flagged, acceptance criteria carried forward.
- `.claude/skills/sdd-implement/SKILL.md` — one task/wave at a time, TDD, fresh session recommended per task; ticks the checklist.
- `.claude/skills/sdd-validate/SKILL.md` — re-checks acceptance criteria fresh, logs drift to `notes.md`, never silently edits spec.
- `specs/README.md` — index template: one row per spec with status and open-question count; documents the viewer.
- `specs/index.html` — viewer and editor. Reads the markdown at load time and holds no copy. Index, per-spec documents, requirements paired with acceptance criteria, a Progress view (three charts, filters, every spec and task), in-browser editing and task ticking.
- `specs/serve.py` — the local server the viewer saves through. Standard library, loopback only, writes only the spec markdown files, refuses a save over a file that changed on disk.

Every skill hard-stops after writing its artifact; none auto-chains to the next.

## Design decisions made (with rationale)
- Added a validate phase — not in Spec Kit/Kiro, pulled from Allegro + Thoughtworks' "re-iterate spec after implementation."
- No skip-gate fast path (Kiro's Quick Spec) — user wants every step human-checked, no exceptions.
- No wave scheduler — `[P]` flag only, concurrent execution left to the human.
- Constitution is a freeform interview grounded in the actual repo, not Spec Kit's fixed 9-article template.
- Code stays the persisted artifact (Spec Kit/Kiro hybrid), not Tessl's fully-regenerable-from-spec model — Thoughtworks' determinism objection was the reason.
- No clause-ID↔test traceability (Sean Grove's Model Spec pattern) — acceptance criteria flow spec→tasks→tests but without stable IDs.
- Context-management rules (file-as-state not conversation, per-feature isolation, fresh session per task) are original additions, not sourced from any reviewed tool.
- The viewer holds no state (2026-10-09). The markdown is the only source; the page is a display and edit form over it. Progress is the checkboxes in `tasks.md`, counted on load, never stored a second time.
- `tasks.md` has a prescribed format (2026-10-09). Free-form task lists could not be counted or ticked reliably — the first one written put its checkboxes in headings. The format is in `sdd-tasks`.
- No one-command pipeline (2026-10-09). Considered and rejected again: it would remove the gates.

## Findings from first real use (2026-10-09)
- **Planning a feature that changes existing files needs those files.** `sdd-plan` says to read only the spec and the constitution and no code. For a spec written after the thing it describes, the plan could not be written without reading the files it changes. The context rule needs an exception for "files this feature modifies".
- **Requirements changed after the plan existed, twice in one session.** `sdd-specify` only creates. The spec was amended by hand and the plan revised after it. There is no amend step, and nothing marks a plan or task list stale when its spec changes.
- **Nothing moves a spec from `draft` to `approved`.** Plans and task lists were written for specs still listed as `draft`. Either a skill does it on the human's word, or the skills stop checking for it.
- **A plan surfaces conflicts the spec has to settle.** Each plan ended with a short list of conflicts for the human; resolving them changed the spec. That loop — plan → conflict → spec amended → plan revised — is not in the pipeline diagram and probably should be.
- **A skill run without a spec name has nothing to go on.** `/sdd-plan` and `/sdd-implement 1` were both run without saying which spec. The skills should ask, or take the lowest-numbered spec at the right stage.
- **Tasks that only a human can do** (anything needing credentials, an outside device, an account setting) turned up in the first task list. The format has no marker for them.

## Known gaps / deliberately not built
- No git branch/issue automation (Spec Kit auto-branches, `taskstoissues`).
- No Design-First workflow variant (Kiro: start from architecture, derive requirements after).
- No spec-quality scoring (Thoughtworks: industry has no consensus metric here).
- No `/sdd-amend`, no approval step — see findings.
- Viewer: does not create, rename or delete files; does not know which artifacts are stale; loads its markdown renderer from a CDN, so it needs network access. Not checked at phone width or in dark mode for the Progress view.

## Next steps (pick up here)
1. Human review of the 6 SKILL.md files + CLAUDE.md themselves.
2. Run implement and validate on a real feature; check task sizing (≤3 files) and gate-stop behavior actually hold up in practice.
3. Decide on the findings above: an amend skill, an approval step, the `sdd-plan` reading exception, a default spec when none is named.
4. Decide whether to add: clause-ID traceability, a wave scheduler, a Design-First variant, or a packaged Spec Kit-style article template for `sdd-constitution`.
5. Decide install mechanism for target repos: plain copy vs. Claude Code plugin packaging.
