# FAQ

## Is C.O.D.E. Loop a software framework?

No.

C.O.D.E. Loop is an operating model for governing AI-assisted software development.

The current repository includes a Markdown-first reference implementation, but the paradigm is not tied to Markdown or to a specific tool.

## Is this just documentation?

No.

Documentation records information.

C.O.D.E. Loop uses artifacts as governance objects. They define what downstream work is allowed to assume, validate and implement.

If artifacts are written but do not govern decisions, the loop is not really being applied.

## Is this waterfall?

No.

C.O.D.E. Loop has ordered layers, but it is not a one-way waterfall process.

Lower layers can produce evidence, mismatch reports and change requests that move back upward.

The point is not linear rigidity.

The point is controlled propagation.

## Does C.O.D.E. Loop replace TDD?

No.

TDD remains useful inside Execution and validation strategy.

TDD asks whether the software is being built correctly against tests.

C.O.D.E. Loop asks whether the work is still building the correct software according to intent, constraints and design rationale.

## Does this slow teams down?

Sometimes.

That friction is useful when the cost of drift is high.

For small local edits, a full loop may be too heavy.

For significant changes, explicit intent, design and validation can prevent much more expensive rework later.

## When should I use the full loop?

Use the full loop when a change affects:

1. behavior;
2. architecture;
3. contracts;
4. data models;
5. validation strategy;
6. operational risk;
7. security or safety;
8. long-term maintainability.

## Can agents create the artifacts?

Yes.

Agents can draft artifacts, identify mismatch, propose changes and run validation checks.

The important constraint is authority.

An agent should not silently change upper-layer intent, scope or success criteria through implementation.

## Can the loop be automated?

Partly.

Some checks can be automated, such as schema completeness, links between artifacts, test evidence and validation state.

Other checks require engineering judgment, especially around intent, tradeoffs and acceptable risk.

## Why not just use ADRs?

ADRs are useful for recording architectural decisions.

C.O.D.E. Loop is broader.

It governs the movement from intent to orchestration, design, execution and validation.

ADRs can live inside a C.O.D.E. Loop workflow, but they do not replace the whole loop.

## Why not just trust tests and CI?

Tests and CI are essential, but they mostly validate behavior and integration.

They do not automatically prove that implementation preserved the original intent or respected architectural boundaries.

C.O.D.E. Loop adds upstream governance.

## What is the smallest useful version?

For a small but significant change, a minimal loop can be:

1. one Concept note;
2. one Design note;
3. one Execution note with tests;
4. one Validation note.

The artifacts can be short.

They just need to make intent, constraints and evidence explicit.

## What is the biggest risk of using C.O.D.E. Loop badly?

Turning it into paperwork.

The loop should clarify decisions, not bury them.

If artifacts become long, vague or ignored, they are not helping.

The goal is not more documents.

The goal is controlled meaning.

