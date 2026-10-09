# Sean Grove — "The New Code" (OpenAI)

**Source:** AI Engineer World's Fair 2025 talk; widely cited as the founding talk of spec-driven development.
**URL (transcript):** https://lawwu.github.io/transcripts/8rABwKRsec4.html
**Type:** Conference talk / thesis piece, not a tool.

## Core Thesis
Code is a **lossy projection of intent**. Writing code is only ~10–20% of a programmer's value; ~80–90% is structured communication of intent, constraints, and goals. In an AI-native workflow, the specification — not the prompt, not the code — is where human intent actually lives, so it should be authored first and kept as the durable artifact. Grove's framing: developers currently "shred the source [the prompt] and carefully version-control the binary [the code]" — backwards.

## Worked example: OpenAI's Model Spec
- A living, natural-language Markdown document, version-controlled like code.
- Readable/debatable by non-engineers (product, legal, safety, research) — a genuine cross-functional alignment tool.
- Each clause carries an ID linked to test prompts that encode pass/fail criteria — i.e., the spec is *executable/testable*, not just descriptive prose.
- Used during the GPT-4 sycophancy incident as a **trust anchor**: the spec let the team say the behavior contradicted stated values, turning an ambiguous bug into a diagnosable misalignment.

## Workflow implied
1. Write the specification first; define success criteria before implementation.
2. Feed the spec to the model as system context (spec becomes executable, not just documentation).
3. Evaluate outputs against the spec as the rubric (ties to OpenAI's "deliberative alignment" training/eval loop).
4. Treat spec authorship as a universal skill — engineers, PMs, and even lawmakers are all "spec authors" aligning a system to intent.

## Do
- Write specs that a non-engineer stakeholder can read and contest.
- Attach concrete test cases/prompts to each clause so the spec is checkable, not aspirational.
- Keep the spec under version control alongside code.
- Use the spec as the arbiter when behavior is ambiguous ("is this a bug or a feature?").

## Don't
- Don't treat the prompt as disposable and the generated code as the permanent record — that inverts where the intent actually lives.
- Don't write specs as unfalsifiable prose with no way to test compliance.
- Don't restrict spec authorship to engineers only — cross-functional input is the point.

## Caveat
This is a vision/thesis talk, not a methodology doc — it argues *why* SDD matters, not the mechanics of *how* to run it day to day (see Spec Kit / Kiro / Tessl files for the operational side).
