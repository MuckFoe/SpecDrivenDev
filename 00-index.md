# Specification-Driven Development — Research Index

Research date: 2026-09-11. Scope: 2025–2026 "AI-native" usage of the term (see file 06 for the distinct pre-LLM 2004 usage).

## Files
| File | Resource | Kind |
|---|---|---|
| [01](01-github-spec-kit.md) | GitHub Spec Kit | OSS tool + methodology doc |
| [02](02-aws-kiro.md) | AWS Kiro | Commercial IDE |
| [03](03-sean-grove-the-new-code.md) | Sean Grove, "The New Code" (OpenAI) | Founding thesis talk |
| [04](04-thoughtworks-analysis.md) | Thoughtworks | Independent critical analysis |
| [05](05-tessl.md) | Tessl | Commercial platform (unverified — fetch failed) |
| [06](06-wikipedia-overview.md) | Wikipedia | Tertiary reference |
| [07](07-allegro-tech-best-practices.md) | Allegro Tech | Practitioner field report |

## Convergent findings (agreed across ≥3 sources)
- Universal 3-phase skeleton: **specify → plan/design → tasks → implement**, with human approval gates between phases.
- Spec = WHAT/WHY (behavior, constraints, acceptance criteria); plan/design = HOW. Mixing these is the most-cited failure mode.
- Specs must be versioned in the repo alongside code, not kept as external/disposable docs — this is *the* mechanism claimed to prevent doc drift.
- Tasks should be decomposed to fit an agent's context window and carry explicit acceptance criteria.
- Human review remains mandatory; no source endorses prompt→merge with no checkpoint.
- Ambiguity should be marked explicitly (Spec Kit's `[NEEDS CLARIFICATION]`, Kiro's Analyze Requirements phase) rather than resolved by agent guessing.

## Open disagreement (unresolved as of this research)
- **Is the spec or the code the true source of truth?** Tessl (05) bets fully on spec-as-source, code as regenerable/disposable. Spec Kit and Kiro keep both, with the spec governing but code persisting normally. Thoughtworks (04) explicitly says the field has no consensus here.
- **Determinism:** SDD's drift-prevention promise assumes regenerating from a spec is reliable. Thoughtworks is the one source that names this as unsolved — LLM codegen isn't deterministic, so CI/CD rigor is still required as a backstop, not a nice-to-have.
- **Term collision:** "spec-driven development" meant TDD+design-by-contract in 2004 (file 06); the 2025 AI-coding meaning is unrelated. Disambiguate when citing externally.

## Cross-source synthesis: Do / Don't
**Do:** write specs collaboratively; separate spec (stable) from plan/tasks (per-change delta); use structured notation (EARS, Given/When/Then, OpenAPI/proto over ad hoc formats); calibrate spec detail to risk; keep specs under version control; require human approval at phase boundaries; decompose into context-sized tasks with acceptance criteria.

**Don't:** put implementation detail in the spec; write specs solo; over-specify (spec becomes pseudo-code) or under-specify ("should work well"); skip re-iterating the spec after implementation changes; let agent self-review replace human review; apply SDD ceremony to trivial/low-risk tasks; assume regenerated code is drift-free without CI/CD backing it up.
