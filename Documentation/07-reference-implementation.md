# Reference Implementation

## Tool-Agnostic Paradigm, Markdown-First Implementation

C.O.D.E. Loop is not Markdown.

The paradigm is the governance model:

```text
Intent -> Artifact -> Validation -> Controlled Propagation -> Software
```

The current repository implements that model with Markdown because Markdown is readable, versionable and easy for both humans and agents to consume.

This is a practical choice, not a permanent constraint.

A future implementation could use structured databases, JSON, YAML, issue trackers, IDE extensions, CI integrations or dedicated agent runtimes.

The important property is not the file format.

The important property is that the work remains explicit, reviewable and governed.

## Repository Structure

The repository separates the paradigm from its implementation.

The foundation documents define:

1. what C.O.D.E. Loop is;
2. what it is not;
3. the glossary;
4. the non-negotiable principles;
5. the governance model.

The model documents define:

1. layer responsibilities;
2. propagation rules;
3. validation gates;
4. escalation types;
5. artifact hierarchy;
6. artifact tree behavior;
7. operational guardrails.

The rule bundles provide concrete operating instructions for agents or teams.

The pilot documents and runs provide preliminary evidence and examples.

The public reference rule bundle is available in:

```text
../MyImplementation/code_loop/
```

## Rule Bundles

The repository currently preserves multiple versions of the rule system.

The first rule bundle defines the basic layer flow.

The second version adds branching, checkpointing and parent-child artifact relationships.

The third version adds stronger operational guardrails, including artifact tree concepts, truthfulness, ambiguity handling, simplicity and intent preservation.

Keeping these versions separate is intentional.

It makes the evolution of the paradigm visible and prevents newer ideas from being confused with older baselines.

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

## Evidence From Pilots

The repository includes comparative pilots with and without C.O.D.E. Loop.

These pilots are not definitive proof.

They are early evidence.

They suggest that the loop improves:

1. visibility of assumptions and constraints;
2. governance discipline;
3. rationale reconstruction;
4. surfacing of risks and mismatches;
5. separation between intent, design and implementation.

They also show a useful tradeoff: a non-loop run may sometimes produce a more complete demo faster, while the loop produces stronger governance and traceability.

That tradeoff matters.

C.O.D.E. Loop should not be sold as magic speed.

It should be understood as a way to keep generated software aligned with meaning.
