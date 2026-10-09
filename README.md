# Spec-Driven Development

A skill-pack for [Claude Code](https://claude.com/claude-code). It turns a
feature idea into code through six steps, each ending in a markdown file a
human approves before the next step starts. It ships a browser viewer for
reading, editing and tracking those files.

## Install

Copy into the root of the target repository:

```
CLAUDE.md             pipeline rules, loaded by Claude Code every session
.claude/skills/sdd-*  the six skills
specs/                README.md (index), index.html (viewer), serve.py (save server)
```

If the target already has a `CLAUDE.md`, merge this one into it.

Needs: Claude Code; Python 3.7+ for the viewer; network access in the browser
(the viewer loads `marked` and `DOMPurify` from cdnjs).

## Pipeline

| # | Command | Reads | Writes | You approve |
|---|---|---|---|---|
| 0 | `/sdd-constitution` | repo standards, your answers | `memory/constitution.md` | the principles. Once per project |
| 1 | `/sdd-specify` | constitution | `specs/<NNN-slug>/spec.md`, a row in `specs/README.md` | the spec, after resolving every `[NEEDS CLARIFICATION]` |
| 2 | `/sdd-plan` | spec, constitution | `plan.md` | the architecture |
| 3 | `/sdd-tasks` | plan, spec | `tasks.md` | the task list |
| 4 | `/sdd-implement` | one task | tests, code, the task's checkbox | the diff, per task |
| 5 | `/sdd-validate` | spec, tasks, test run | `notes.md` (appended) | the feature |

Rules that hold at every step:

- **A skill stops after writing its file.** It never runs the next one. You do.
- **State lives in files, not in the conversation.** You can clear the session
  between any two steps.
- **A skill reads only its declared inputs.** Never other features' files.
- **Ambiguity is marked, never guessed:** `[NEEDS CLARIFICATION: <question>]`.
- **Spec is WHAT and WHY. Plan is HOW.** No tech stack, file or API in a spec.
- **A change in behaviour changes the spec first.**
- **Not for a trivial one-file fix.**

## What each file contains

**`memory/constitution.md`** — short, numbered, checkable rules every plan must
satisfy: testing discipline, architecture boundaries, integration versus mocked
tests, fixed stack constraints, anything that blocks a plan outright.

**`spec.md`** — exactly these sections:

| Section | Content |
|---|---|
| Problem / Why | the need, one paragraph |
| Users | who it is for |
| Functional requirements | EARS: `WHEN <trigger> THE SYSTEM SHALL <response>`, as `- **FR1** — …` |
| Non-functional requirements | performance, security, scale, where they matter |
| Out of scope | explicit exclusions |
| Acceptance criteria | Given/When/Then, one per requirement, keyed by the same id |
| Open questions | `[NEEDS CLARIFICATION: …]` markers |

**`plan.md`** — architecture, data model, contracts precise enough to code
from, test strategy mapping each acceptance criterion to a test, and
constitution compliance rule by rule with conflicts flagged for you. Every
decision traces to a requirement.

**`tasks.md`** — fixed format; progress is recorded here and nowhere else:

```markdown
## Waves
| Wave | Tasks | Why this order |
|---|---|---|
| 1 | 1 | … |
| 2 | 2, 3 — all `[P]` | … |

## Checklist
- [ ] **1** — <title>
- [ ] **2** — `[P]` <title>

## Tasks
### 1. <title>
- **Plan:** <component>. **Spec:** FR1, FR3.
- **Files:** … **Depends on:** … **Do:** …
- **Acceptance:** <criterion from the spec, and how this task checks it>
```

- One task is one concern and about three files at most.
- `[P]` marks a task with no unfinished dependency; `[P]` tasks of one wave can
  run together. Running them concurrently is up to you.
- One checkbox per task, in the checklist only, never in a heading. Every
  `- [ ]` in the file counts as a task.
- The task number links the checklist line, the waves table and the heading.

**`notes.md`** — appended on each validation run: drift and learnings, each
flagged as "spec.md is now stale on: …". `/sdd-validate` runs the tests,
reports pass or fail per acceptance criterion against actual behaviour, and
never edits the spec itself.

**`specs/README.md`** — the index: number, linked spec, summary, status, count
of open questions. Status is `draft`, `approved`, `planned`, `in progress` or
`validated`; only you move a spec out of `draft`. Numbers are never reused.

## Implementing

`/sdd-implement` takes one task, or one `[P]` wave, per run:

1. Stops if a dependency is not ticked.
2. Writes the test from the task's acceptance criteria and sees it fail.
3. Implements the minimum that passes it.
4. Ticks the task in the checklist.

Use a fresh session per task. If implementation shows the spec or plan is
wrong, the skill stops and says so instead of diverging.

## Viewer

```
python specs/serve.py [port]      default 8777, then http://127.0.0.1:8777/
```

The page reads the markdown under `specs/` on every load and keeps no copy.

| View | Shows |
|---|---|
| Index | every spec: status, open questions, which of spec / plan / tasks / notes exist; unresolved markers; a text filter |
| Spec | one tab per file; requirements paired with their acceptance criteria |
| Progress (`#progress`) | tasks done per spec, specs per artifact, tasks per wave, and every spec with every task. Filters: text, status, artifact, open or done, only `[P]` |

**Editing.** Every file has an **Edit** button; **Save** or Ctrl+S writes the
whole file. Task checkboxes are clickable.

- A save writes to the working tree, uncommitted. Git is the undo.
- A save over a file that changed on disk since the page read it is refused.
- It edits existing files only. It does not create, rename or delete.
- It does not know the pipeline: editing a spec marks nothing stale.

**`serve.py`** uses the standard library only, binds `127.0.0.1`, refuses to
start on a busy port, and accepts writes only to `README.md` and
`<folder>/{spec,plan,tasks,notes}.md`, only from its own page. Under any other
static server the page works read-only.

## Not included

- An amend step: `/sdd-specify` only creates; changing a spec is a manual edit,
  after which its plan and tasks are yours to revise.
- A step that sets a spec's status.
- Git branch or issue automation, a wave scheduler, a design-first variant,
  spec-quality scoring, stable links from requirement ids to tests.

## In this repository

| Path | What |
|---|---|
| `CLAUDE.md`, `.claude/skills/`, `specs/` | the pack |
| `STATE.md` | design decisions with reasons, findings from first use, next steps |

Status: used on one project through specify, plan and tasks. Implement and
validate are untested in practice.
