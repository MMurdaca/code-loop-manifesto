# Adoption Modes

C.O.D.E. Loop should be proportional to the risk of the change.

The goal is not to force every edit through the same amount of structure.

The goal is to make intent, design and validation explicit enough for the work being done.

## Tiny Mode

Use Tiny Mode for small changes that still deserve traceability.

Good fit:

1. local behavior changes;
2. small bug fixes with clear scope;
3. documentation or test updates with limited risk;
4. low-risk refactors inside one component.

Minimum artifacts:

1. one short intent note;
2. one execution note with evidence;
3. one validation note.

Tiny Mode is enough when the change does not alter architecture, public contracts, data relationships, invariants or operational risk.

Example folder:

```text
code-loop/
  intent.md
  execution.md
  validation.md
```

## Standard Mode

Use Standard Mode for meaningful product or engineering work.

Good fit:

1. new features;
2. changes affecting observable behavior;
3. changes involving more than one module;
4. work that needs clear design rationale;
5. agent-assisted implementation where scope drift is plausible.

Minimum artifacts:

1. Concept;
2. Orchestration;
3. Design;
4. Execution;
5. Validation.

Standard Mode is the default recommended mode for adopting C.O.D.E. Loop.

Example folder:

```text
code-loop/
  artifact-tree.md
  concept.md
  orchestration.md
  design.md
  execution.md
  validation.md
```

## Strict Mode

Use Strict Mode when silent drift would be expensive, risky or hard to detect after the fact.

Good fit:

1. architecture changes;
2. public API or contract changes;
3. data model changes;
4. identity, identifier or relationship changes;
5. security, safety, finance, audit or compliance-sensitive work;
6. multi-agent or long-running work where context can fragment.

Strict Mode adds:

1. explicit artifact tree tracking;
2. branch, parent or layer gates when scope branches;
3. drift policy mode: `Mitigate`, `Review` or `Strict`;
4. escalation when a lower layer finds mismatch;
5. explicit approval or re-validation before contract-changing execution.

Example folder:

```text
code-loop/
  artifact-tree.md
  artifacts/
    A1-concept.md
    A1.1-orchestration.md
    A1.1.1-design.md
    A1.1.1.1-execution.md
    A1.1.1.1.V1-validation.md
    A1.1.R1-drift-review.md
```

## Choosing A Mode

Use the smallest mode that still protects the meaning of the work.

Choose Tiny when the change is local and reversible.

Choose Standard when the change needs visible reasoning across intent, design and implementation.

Choose Strict when the change can alter contracts, identity, relationships, invariants, auditability, safety or long-term architecture.

## Mode Escalation

A task can start in Tiny or Standard Mode and move upward.

Escalate the mode when:

1. implementation reveals ambiguity in intent;
2. design finds a contract or invariant issue;
3. a new request changes an approved assumption;
4. validation cannot prove that upstream intent is preserved;
5. an agent wants to simplify by changing architecture or data semantics.

Mode escalation is not a failure.

It is the loop doing its job.
