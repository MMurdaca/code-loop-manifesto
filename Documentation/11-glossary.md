# Glossary

## C.O.D.E. Loop

An artifact-driven operating model for AI-assisted software development.

It organizes significant work through Concept, Orchestration, Design and Execution, with validation and controlled propagation between layers.

## Intent

The explicit statement of what the system or change is trying to achieve.

Intent includes goals, constraints, assumptions, success criteria and out-of-scope boundaries.

## Artifact

An explicit, reviewable object that captures decisions, constraints, output or validation state.

An artifact can be a Markdown file, structured document, issue, database record or another readable representation.

## Concept

The layer that defines the intent.

It answers:

```text
What are we trying to achieve, and what must remain true?
```

## Orchestration

The layer that turns intent into work structure.

It defines responsibilities, dependencies, sequencing, risks and coverage of the Concept.

## Design

The layer that turns orchestration into implementable constraints.

It defines contracts, interfaces, models, invariants, edge cases and validation strategy.

## Execution

The layer that produces concrete software.

It implements within the approved design and produces evidence, tests, mismatch reports and deviation notes.

## Validation Gate

A check that decides whether an artifact can propagate or continue.

Common outcomes:

1. Pass;
2. Pass with Conditions;
3. Fail.

## Controlled Propagation

The movement of validated information from one layer to the next.

Controlled propagation prevents downstream work from relying on vague, implicit or unvalidated assumptions.

## Escalation

The process by which a lower layer reports ambiguity, mismatch, conflict or improvement opportunity to an upper layer.

Escalation allows lower layers to challenge upstream decisions without silently rewriting them.

## Adoption Mode

The chosen level of C.O.D.E. Loop structure for a task.

The public modes are Tiny, Standard and Strict.

## Tiny Mode

A lightweight mode for local, low-risk changes that still need traceability.

## Standard Mode

The default mode for meaningful product or engineering work that needs visible intent, design, execution and validation.

## Strict Mode

A stronger mode for architecture, contracts, data models, identity, relationships, invariants, auditability, safety, security or other high-risk changes.

## Architectural Contract Drift

A change that alters an approved identity, identifier, relationship, invariant, validation criterion or shared contract.

This is especially important when code can keep working while meaning or auditability degrades.

## Drift Policy Mode

The policy used when architectural contract drift is detected.

Allowed modes are `Mitigate`, `Review` and `Strict`.

## Rushed Execution

The failure mode where implementation begins before intent, constraints, responsibilities and success criteria are explicit enough.

## AI Code Inflation

The accumulation of generated code that is locally plausible but globally under-governed.

It can create hidden dependencies, abstraction leakage and fragile rationale.

## Drift

The gradual loss of alignment between intent, architecture, design and implementation.

Common forms include requirement drift, architectural drift, context drift and validation drift.

## Artifact Tree

A structure that organizes parent and child artifacts when work branches into multiple scopes.

The tree makes lineage, state and coverage visible.

## Parent Artifact

The upstream artifact that governs a downstream artifact.

## Child Artifact

An artifact created from a parent artifact to cover a declared part of the parent scope.

## Branch

A traceable path of work connecting parent and child artifacts.

Branches are useful when one artifact is too large to validate as a single unit.

## Evidence

Information produced to support validation, escalation or decision-making.

Evidence may include tests, logs, analysis, constraints, observed mismatch or reasoning.

## Reference Implementation

The current Markdown-first implementation of C.O.D.E. Loop in this public package.

It is one implementation of the paradigm, not the paradigm itself.
