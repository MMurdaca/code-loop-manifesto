# Reference Implementation

## Tool-Agnostic Paradigm, Markdown-First Implementation

C.O.D.E. Loop is not Markdown.

The paradigm is the governance model:

```text
Intent -> Artifact -> Validation -> Controlled Propagation -> Software
```

This public package implements that model with Markdown because Markdown is readable, versionable and easy for both humans and agents to consume.

This is a practical choice, not a permanent constraint.

A future implementation could use structured databases, JSON, YAML, issue trackers, IDE extensions, CI integrations or dedicated agent runtimes.

The important property is not the file format.

The important property is that the work remains explicit, reviewable and governed.

## Standalone Package Structure

The public package separates explanation, rules and evidence recap.

`Documentation/` explains:

1. what C.O.D.E. Loop is;
2. what problem it addresses;
3. the four-layer model;
4. validation and escalation;
5. adoption modes;
6. limits and open questions.

`MyImplementation/code_loop/` contains the current public reference rule bundle.

`MyImplementation/Result/` contains a standalone recap of the evidence collected so far.

This package is intended to remain readable without material outside this public directory.

## Current Public Rule Bundle

The public rule bundle is the current Markdown-first implementation.

It includes:

1. the Concept, Orchestration, Design and Execution layer rules;
2. validation gates;
3. escalation rules;
4. artifact schema rules;
5. artifact tree concepts;
6. checkpointing and parent-child lineage;
7. guardrails for truthfulness, ambiguity handling, simplicity and intent preservation;
8. architectural contract drift handling for identity, identifiers, relationships, invariants and shared contracts.

The public drift policy modes are:

1. `Mitigate`: proceed only with documented mitigation, explicit conditions and suitable validation;
2. `Review`: pause and request approval or parent re-validation before implementation;
3. `Strict`: block execution until upstream contract revision and re-validation happen.

When no local drift policy is declared, the default is `Review`.

## Artifacts

Artifacts are the central unit of the implementation.

An artifact can describe:

1. intent;
2. orchestration;
3. design;
4. execution evidence;
5. validation result;
6. escalation;
7. decision history.

In the Markdown-first implementation, artifacts are human-readable documents.

They are structured enough to guide agents, but not so rigid that humans need a parser to understand the project.

## Validation And Escalation

The reference implementation includes validation gates and escalation protocols.

Validation gates decide whether an artifact can propagate.

Escalation protocols define how a lower layer reports ambiguity, conflict, mismatch or improvement opportunities to a higher layer.

The goal is to prevent silent drift.

A lower layer can challenge an upper layer.

It just has to do so explicitly.

## Evidence Recap

The public package does not require raw pilot folders to be useful.

A standalone evidence recap is available in:

```text
../MyImplementation/Result/README.md
```

The evidence is preliminary.

It suggests that the loop improves:

1. visibility of assumptions and constraints;
2. governance discipline;
3. rationale reconstruction;
4. surfacing of risks and mismatches;
5. separation between intent, design and implementation.

It also shows a useful tradeoff: a non-loop run may sometimes produce a more complete demo faster, while the loop produces stronger governance and traceability.

That tradeoff matters.

C.O.D.E. Loop should not be sold as magic speed.

It should be understood as a way to keep generated software aligned with meaning.
