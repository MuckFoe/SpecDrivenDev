# Thoughtworks — "Spec-Driven Development: Unpacking 2025's Key New Engineering Practice"

**Source:** Thoughtworks Insights blog
**URL:** https://www.thoughtworks.com/en-us/insights/blog/agile-engineering-practices/spec-driven-development-unpacking-2025-new-engineering-practices
**Type:** Independent critical analysis (consultancy), not a tool vendor.

## Positioning
SDD is framed as the corrective to "vibe coding" (too fast, spontaneous, haphazard) — reintroducing structure without reverting to full waterfall. Value comes from separating planning from implementation to get faster, tighter feedback loops than unstructured AI generation.

## Named risks (this is the most skeptical source found)
- **Non-determinism:** LLM spec→code generation isn't deterministic, which complicates upgrades and long-term maintenance — regenerating from an unchanged spec is not guaranteed to reproduce the same code.
- **Spec drift & hallucination:** called "inherently difficult to avoid" — deterministic CI/CD is still required as a backstop, SDD doesn't remove the need for it.
- **No consensus / no evaluation framework:** there is not yet an agreed way to measure "spec quality," and the field is still split on whether the spec or the code is the true source of truth.

## Recommended practices
- Formalize requirements into structured Markdown during a distinct planning phase, separated from implementation.
- Human-in-the-loop review of the spec *before* code generation starts.
- Define architecture/constraints/coding standards upfront in an `AGENTS.md`-style technical spec.
- Keep CI/CD rigor high regardless of SDD — it's a complement, not a replacement.

## Do
- Use domain/ubiquitous language in specs (DDD-style), not ad hoc wording.
- Structure specs with Given/When/Then (BDD) scenarios.
- Apply context-engineering discipline — curate what's fed to the model rather than dumping everything.
- Combine natural language with semi-structured formats (tables, schemas) rather than pure prose.

## Don't
- Don't rely on functional requirements alone — omitting technical/non-functional detail causes drift.
- Don't over-formalize specs to the point they slow down change and feedback cycles (reintroducing waterfall's core failure mode).
- Don't treat specs as disposable/one-time documents — they need ongoing maintenance like code.
- Don't drop traditional engineering discipline (testing, CI/CD, review) on the assumption SDD substitutes for it.
