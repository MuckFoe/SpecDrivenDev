# Tessl (Spec Registry + Framework)

**Source:** Tessl product/docs and press coverage (founded by Guy Podjarny, Snyk founder; ~$125M raised)
**URLs:** https://tessl.io/ , https://docs.tessl.io/introduction-to-tessl/concepts , https://docs.tessl.io/use/spec-driven-development-with-tessl
**Type:** Commercial platform (Spec Registry — open beta; Tessl Framework — private beta).
**Note:** `docs.tessl.io` was unreachable at research time (DNS timeout); this file is based on search-indexed summaries of the docs and third-party coverage, not a direct fetch — treat specifics as lower-confidence than the other files here and re-verify before relying on them.

## Core Claim (the most radical of the sources reviewed)
Inverts the usual relationship entirely: **the spec is the artifact you maintain; the code becomes a regenerable, disposable output.** Generated files are stamped `// GENERATED FROM SPEC - DO NOT EDIT`. Tests are bound to spec assertions, not written independently.

## Workflow
1. AI coding agent gathers requirements and drafts specs (not code) first.
2. Human reviews and approves the specs.
3. Agent implements from the approved spec.
4. Specs are committed alongside code and tests, functioning as versioned long-term memory: why a feature exists, how it should behave, what "correct" means.
5. When behavior needs to change, the spec is edited first; code regenerates from it — this is the mechanism that is supposed to keep spec and code from drifting apart (contrast with Thoughtworks' skepticism that drift is avoidable at all).

## Do
- Commit specs to the repo alongside code and tests, versioned together — not as separate/external docs.
- Treat the spec as the unit of change: edit the spec, then regenerate, rather than hand-patching generated code.
- Use specs as onboarding/institutional memory (why a feature exists), not just as a pre-code checklist.

## Don't
- Don't hand-edit files marked as generated-from-spec — edits will be lost/inconsistent on regeneration.
- Don't let specs live outside version control or outside the repo — that's the exact "docs that drift" failure mode SDD is trying to fix.
- Don't treat this model as risk-free: full regenerate-on-spec-change assumes deterministic, faithful codegen, which is precisely what Thoughtworks (file 04) flags as unresolved for LLMs today.
