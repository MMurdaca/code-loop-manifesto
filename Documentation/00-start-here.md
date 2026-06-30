# Start Here

C.O.D.E. Loop is a proposal for governing AI-assisted software development.

It is built around one core concern:

```text
code can now be generated faster than intent can be validated.
```

This creates a new kind of engineering risk. A coding agent can produce working software while silently changing scope, architecture, assumptions or design rationale.

C.O.D.E. Loop tries to prevent that silent drift.

## The Core Idea

Significant software work should move through a visible chain:

```text
Intent -> Artifact -> Validation -> Controlled Propagation -> Software
```

This means:

1. clarify the intent before implementation;
2. capture decisions in artifacts, not only in conversation;
3. validate artifacts before using them downstream;
4. let lower layers report evidence and mismatch;
5. prevent implementation from silently rewriting upper-layer intent.

## The Four Layers

C.O.D.E. Loop uses four governed layers.

Concept:

defines the problem, goals, constraints, assumptions and success criteria.

Orchestration:

turns intent into work structure, responsibilities, dependencies, sequencing and risks.

Design:

defines contracts, interfaces, models, invariants, edge cases and validation strategy.

Execution:

implements the design and produces evidence, tests, mismatch reports and integration notes.

## Use It Proportionally

C.O.D.E. Loop has adoption modes.

Tiny Mode is for small local changes that still deserve traceability.

Standard Mode is for meaningful work that needs visible intent, design and validation.

Strict Mode is for architecture, contracts, identity, data relationships, auditability, safety or other high-risk changes.

The right mode is the smallest one that still protects the meaning of the work.

## What This Is Not

C.O.D.E. Loop is not a replacement for:

1. TDD;
2. Agile;
3. ADRs;
4. CI;
5. DevOps;
6. version control;
7. code review.

Those practices remain useful.

C.O.D.E. Loop adds a governance layer above implementation.

## What To Read Next

For the argument:

1. `01-abstract.md`
2. `03-the-problem.md`
3. `04-the-code-loop-model.md`

For practical use:

1. `12-getting-started.md`
2. `13-minimal-example.md`
3. `15-adoption-modes.md`
4. `../MyImplementation/code_loop/README.md`

For terms:

1. `11-glossary.md`
