# Getting Started

This guide shows how to try C.O.D.E. Loop on a small but meaningful software change.

The goal is not to create paperwork.

The goal is to make the path from intent to implementation visible.

## When To Use The Loop

Use C.O.D.E. Loop when a change may affect:

1. observable behavior;
2. architecture;
3. contracts or interfaces;
4. data models;
5. validation strategy;
6. operational risk;
7. long-term maintainability;
8. agent autonomy.

For tiny local edits, the full loop may be unnecessary.

## Step 1: Define The Concept

Before implementation, write a short Concept artifact.

It should answer:

1. what problem is being solved;
2. what the objective is;
3. what constraints apply;
4. what assumptions are being made;
5. how success will be judged;
6. what is out of scope.

Keep it short, but make it explicit.

## Step 2: Orchestrate The Work

Turn the Concept into a work structure.

Write down:

1. main tasks or responsibilities;
2. dependencies;
3. sequencing;
4. risks;
5. what part of the Concept is covered.

If the work is too broad, split it into branches.

## Step 3: Design Before Execution

Define the design constraints before code is generated.

Write down:

1. interfaces;
2. data or domain models;
3. invariants;
4. edge cases;
5. validation or test strategy;
6. implementation boundaries.

This is where many AI-assisted mistakes should be caught.

## Step 4: Execute Within The Design

Now implement.

Execution should produce:

1. implemented scope;
2. tests or validation evidence;
3. deviations from the design;
4. unresolved issues;
5. detected mismatches.

If implementation reveals that the design is wrong, do not silently rewrite the design through code.

Open an escalation or re-validation.

## Step 5: Validate

Check whether the implementation still matches the upstream artifacts.

Ask:

1. does the code satisfy the Design?
2. does the Design still satisfy the Orchestration?
3. does the Orchestration still preserve the Concept?
4. are assumptions still valid?
5. are risks and mismatches visible?

## Minimal Folder Pattern

A simple project can start with:

```text
code-loop/
  artifact-tree.md
  concept.md
  orchestration.md
  design.md
  execution.md
  validation.md
```

The exact filenames do not matter.

The lineage and validation state matter.

## Using The Reference Rules

The reference rule bundle is available here:

```text
../MyImplementation/code_loop/
```

Recommended reading order:

1. `README.md`
2. `00-principles.md`
3. `10-concept.md`
4. `20-orchestration.md`
5. `30-design.md`
6. `40-execution.md`
7. `50-validation-gates.md`
8. `60-escalation.md`
9. `70-artifact-schema.md`

