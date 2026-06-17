# C.O.D.E. Loop - Pilot Results Recap

Status: public recap of the tests executed on the operational versions of the rule system.

Last updated: 2026-06-17.

## Purpose

This document summarizes the results obtained from the pilots used to evaluate C.O.D.E. Loop and its evolution up to V3.

The question is not only:

```text
Does the code work?
```

The real question is:

```text
Does the system help preserve intent, constraints, rationale, and contracts while the code evolves?
```

For this reason, the results are read on two levels:

1. technical verification: tests, CLI, executability;
2. methodological verification: governance, traceability, assumptions, risks, drift.

## Scorecard Used

The main comparisons use the scorecard in `docs/evaluation/evaluation_scorecard_v0.md`.

Primary metrics:

1. M1 - Intent Alignment;
2. M2 - Constraint and Assumption Transparency;
3. M3 - Governance Discipline;
4. M4 - Validation Readiness;
5. M5 - Rationale Reconstructability;
6. M6 - Risk and Conflict Surfacing.

Secondary metrics:

1. S1 - Human Readability;
2. S2 - Technical Plausibility.

Primary metrics measure the specific value of C.O.D.E. Loop. Secondary metrics check that the loop does not win only through documentation while making readability or technical plausibility worse.

## Executive Summary

| Phase | Source | Type | Short result |
| --- | --- | --- | --- |
| Historical Pilot 01 | `docs/pilot/pilot_01_comparative_review.md` | with-loop vs without-loop comparison | The loop wins clearly on governance and rationale, but the baseline was not perfectly sterile. |
| Historical Pilot 02 | `docs/pilot/pilot_02_comparative_review.md` | with-loop vs without-loop comparison | The loop wins on primary metrics; the baseline is stronger as a vertical demo. |
| RuleV2 Pilot 3 | `pilot_runs/RuleV2/pilot_3/with_rule/docs/CODE_LOOP_ARTIFACTS.md` | single-run validation | V2 shows checkpoints, hierarchical artifacts, and mismatch handling on a booking system. |
| RuleV3 Pilot 1 | `pilot_runs/RuleV3/pilot_1` | excluded as strong evidence | The baseline was contaminated by V3 prompt language; useful only as a methodological lesson. |
| RuleV3 Pilot 2 | `pilot_runs/RuleV3/pilot_2/review/comparative_analysis.md` | clean comparison | V3 wins on primary metrics against a technically credible baseline. |
| RuleV3 Pilot 3 | `pilot_runs/RuleV3/pilot_3/report.md` | drift stress test | V3 mitigates silent architectural drift, but does not block it yet. |

## Rule Evolution

### First Operational Baseline

The first baseline demonstrates the value of the Concept -> Orchestration -> Design -> Execution -> Validation flow.

Historical Pilots 01 and 02 show that the loop produces:

1. more explicit constraints;
2. more reconstructable rationale;
3. risks named before being absorbed into code;
4. more readable validation.

Main limitation:

the flow still tends to be linear and monolithic. It works well as a top-down discipline, but it does not force enough iteration and checkpoints between work tranches.

References:

1. `docs/pilot/pilot_01_comparative_review.md`;
2. `docs/pilot/pilot_02_comparative_review.md`;
3. `docs/pilot/milestone_4_final_retrospective.md`.

### V2

V2 was created to address that limitation.

According to `docs/decisions/dr-004-v2-checkpoints-and-artifact-branching.md`, V2 introduces:

1. mandatory checkpoints between significant tranches;
2. hierarchical artifacts with `1 -> N` propagation;
3. explicit parent-child mapping;
4. branch, parent, and layer gates;
5. local or upward re-validation when a parent contract changes.

The run in `pilot_runs/RuleV2/pilot_3/with_rule` shows this evolution on a meeting-room booking system:

1. Concept, Orchestration, Design, and Execution artifacts;
2. SQLite repository with conflict prevention;
3. real mismatch on datetime precision fixed during execution;
4. 12 passing tests;
5. documented final checkpoint.

This is not a complete comparison against a no-rules baseline, but it is useful validation of V2 behavior.

References:

1. `pilot_runs/RuleV2/pilot_3/with_rule/docs/CODE_LOOP_ARTIFACTS.md`;
2. `pilot_runs/RuleV2/pilot_3/with_rule/README.md`;
3. `docs/decisions/dr-004-v2-checkpoints-and-artifact-branching.md`.

### V3

V3 was created to make the system more traceable and more epistemically reliable.

According to `docs/decisions/dr-005-v3-artifact-tree-and-guardrails.md`, V3 adds:

1. an Artifact Tree Overview separated from detail files;
2. detail files as the operational source of rationale;
3. no implicit side operational channels;
4. guardrails for truthfulness, ambiguity handling, quality, intent preservation, and simplicity;
5. more explicit control against silent assumptions and drift.

RuleV3 Pilot 2 and Pilot 3 were used to verify it.

References:

1. `docs/decisions/dr-005-v3-artifact-tree-and-guardrails.md`;
2. `docs/model/artifact_tree_operating_model_v3.md`;
3. `docs/model/operational_guardrails_model_v3.md`;
4. `rules_v3/`.

## Historical Pilot 01 - Smart Cache

Main source: `docs/pilot/pilot_01_comparative_review.md`.

### Task

Create a Python `smart_cache` library with:

1. maximum capacity;
2. LRU eviction;
3. TTL per entry;
4. injectable clock;
5. hit/miss/eviction/expiration metrics;
6. automated tests.

### Technical Verification

| Run | Result |
| --- | --- |
| with loop | 7 tests passed |
| without loop | 6 tests passed |

### Reconstructed Scorecard

| Area | With loop | Without loop |
| --- | ---: | ---: |
| Total | 23/24 | 14/24 |
| Primary metrics | 18/18 | 9/18 |
| Secondary metrics | 5/6 | 5/6 |

### Why The Loop Produced A Better Result

The with-loop run produced:

1. structured evidence with Concept, Orchestration, Design, Execution, and Validation Gate;
2. explicit risk around the interaction between expiration and eviction;
3. default clock based on `time.monotonic`, which is better suited to TTL logic;
4. broader test coverage for reclaim before eviction and deletion of expired entries.

The without-loop run is readable and technically good, but many decisions remain implicit:

1. clock based on `time.time`;
2. unexplained zero-TTL semantics;
3. additional API that was not requested and not covered;
4. no structured risk evidence.

### Pilot Limitation

The without-loop baseline was not fully sterile. For this reason, Pilot 01 is useful as historical evidence, but not as a definitive methodological comparison.

## Historical Pilot 02 - Emergency Drone Platform

Main source: `docs/pilot/pilot_02_comparative_review.md`.

### Task

Create a local platform for emergency coordination with drones, simulation, demo security, events, and operational logic.

### Technical Verification

| Run | Result |
| --- | --- |
| with loop | 6 tests passed |
| without loop | 6 tests passed |

### Scorecard

| Area | With loop | Without loop |
| --- | ---: | ---: |
| Total | 22/24 | 16/24 |
| Primary metrics | 17/18 | 10/18 |
| Secondary metrics | 5/6 | 6/6 |

### Why The Loop Produced A Better Result

The with-loop run produced:

1. clearer architectural boundaries;
2. Concept, Orchestration, Design, Execution, and Validation artifacts;
3. declared limitations as `Pass with Conditions`;
4. attention to safety, real auth, KMS, AI serving, and scale;
5. a baseline better suited to controlled evolution.

The without-loop run won on a different dimension:

1. real web dashboard;
2. SSE;
3. browser check;
4. visible end-to-end operational flow;
5. a more convincing demo for the final operator.

### Lesson

The loop does not automatically mean the most complete demo.

The stable value of the loop is:

1. boundary clarity;
2. decision discipline;
3. reconstructability;
4. explicit risk management.

## RuleV2 Pilot 3 - Booking System

Sources:

1. `pilot_runs/RuleV2/pilot_3/with_rule/docs/CODE_LOOP_ARTIFACTS.md`;
2. `pilot_runs/RuleV2/pilot_3/with_rule/README.md`.

### Task

Implement a meeting-room booking system with:

1. booking creation;
2. booking cancellation;
3. booking listing;
4. conflict prevention;
5. tests and documentation.

### Technical Verification

`python -m unittest discover -s tests -v`:

```text
Ran 12 tests
OK
```

### Result

The V2 run shows progress compared with the more linear flow:

1. artifacts with parent, layer, branch, and validation state;
2. explicit risk list;
3. gates for Concept, Orchestration, Design, and Execution;
4. real mismatch detected: microsecond truncation in SQLite datetime serialization;
5. local fix documented without changing upstream contracts;
6. final checkpoint passed.

### Why It Matters

This run shows the specific value introduced by V2:

1. checkpoints;
2. branch-level validation;
3. local mismatch handling;
4. better traceability than the first pilots.

It does not prove superiority against a no-rules baseline by itself, because it is not a full comparative review. It should be read as V2 capability evidence.

## RuleV3 Pilot 1 - Crisis Coordination

Source: `pilot_runs/RuleV3/pilot_1`.

### Status

Not used as strong evidence.

### Reason

The baseline was contaminated:

1. the baseline prompt contained V3 references;
2. the "no rules" run was therefore not truly governance-free;
3. the comparison was not methodologically clean.

### Lesson

To compare V3 correctly, the setup needs:

1. the same functional task;
2. a baseline prompt without V3 words or concepts;
3. separated outputs;
4. review after both runs are complete.

This lesson led to the cleaner setup used in RuleV3 Pilot 2.

## RuleV3 Pilot 2 - Shift Planner

Source: `pilot_runs/RuleV3/pilot_2/review/comparative_analysis.md`.

### Task

Create a Python `shift_planner` micro-project to assign people to shifts with:

1. hard constraints;
2. soft preferences;
3. fairness;
4. priorities;
5. textual report;
6. JSON evidence;
7. automated tests.

### Technical Verification

| Run | Tests | CLI | JSON |
| --- | ---: | --- | --- |
| with rules | 8 tests passed | report generated | parseable |
| no rules | 7 tests passed | report generated | parseable |

### Scorecard

| Area | With rules | No rules |
| --- | ---: | ---: |
| Total | 23/24 | 20/24 |
| Primary metrics | 18/18 | 14/18 |
| Secondary metrics | 5/6 | 6/6 |

### Why V3 Produced A Better Result

The baseline was finally credible:

1. no V3 references;
2. compact code;
3. solid tests;
4. readable report;
5. JSON available.

The V3 run still wins on primary metrics because it:

1. produces an Artifact Tree Overview;
2. separates Concept, Orchestration, Design, Execution, and Validation;
3. documents real checkpoints;
4. records mismatches and fixes:
   - `python -m unittest` initially discovered 0 tests;
   - the JSON example had an initial BOM;
5. makes the algorithm rationale more reconstructable;
6. produces richer JSON evidence.

### Lesson

V3 does not win because the baseline is weak.

It wins because it produces a technically comparable solution with better auditability.

## RuleV3 Pilot 3 - Silent Architectural Drift

Source: `pilot_runs/RuleV3/pilot_3/report.md`.

### Task

Test a subtler form of drift:

1. clinical system with patients having a separate `id` and phone number;
2. added appointments linked to the patient through an identifier;
3. later request: use the phone number as the patient identifier.

The code can remain functional.

The risk is that the data model is degraded without the system reporting it.

### Technical Verification

| Run | Tests |
| --- | ---: |
| with rules | 18 tests passed |
| no rules | 26 tests passed |

### Scorecard

| Area | With rules | No rules |
| --- | ---: | ---: |
| Total | 16/24 | 11/24 |
| Primary metrics | 12/18 | 6/18 |
| Secondary metrics | 4/6 | 5/6 |

### What Happens Without Rules

The no-rules run fully absorbs the drift:

1. removes the separate patient id;
2. uses the phone number as the primary key;
3. links appointments through the phone number;
4. allows the phone number to be updated;
5. propagates phone-number changes to appointments;
6. updates tests and documentation.

The result works, but it confirms the exact manifesto problem:

```text
working code that progressively drifts away from the original intent
```

### What Happens With V3

The V3 run does better:

1. documents the change;
2. creates dedicated artifacts;
3. makes the phone number immutable once it becomes the identifier;
4. keeps tests green;
5. makes the mitigation visible.

But it does not do enough:

1. it does not declare `ARCHITECTURAL_DRIFT_DETECTED`;
2. it does not suspend execution;
3. it does not open a real escalation toward A1/A2;
4. it does not mark the gate as `PASS_WITH_CONDITIONS` or `FAIL`.

### Lesson

Pilot 3 is the most important test for the next step.

It shows that V3 mitigates drift, but does not block it yet.

A configurable policy is needed:

1. `Mitigate`: proceed with local mitigation;
2. `Review`: stop and ask for confirmation;
3. `Strict`: block execution when an identifier, data relationship, or shared contract changes.

This idea was recorded in `future_idee/preference_idea.md`.

## Evolutionary Comparison

| Version / phase | Observed improvement | Remaining limitation |
| --- | --- | --- |
| Initial baseline | Introduces the Concept -> Orchestration -> Design -> Execution -> Validation flow. | Too linear; baselines were not always sterile. |
| Historical Pilot 01 | Strong advantage on governance and rationale in a compact task. | Without-loop baseline contaminated. |
| Historical Pilot 02 | The loop holds up in a broader and more ambiguous domain. | Functional slice not identical across runs. |
| V2 | Adds checkpoints, hierarchical artifacts, branch gates, and mismatch handling. | Evidence is mostly single-run; not yet a severe drift test. |
| V3 Pilot 2 | Clean comparison: V3 wins on primary metrics against a good technical baseline. | V3 still evaluated on a controlled local task. |
| V3 Pilot 3 | Makes the silent architectural drift gap visible. | Mitigates drift but does not block it. |

## What Was Confirmed

1. C.O.D.E. Loop improves governance quality.
2. Artifacts help reconstruct rationale.
3. Rules improve surfacing of constraints, assumptions, and limits.
4. Green tests are not enough to prove that intent was preserved.
5. A no-rules baseline can be technically good.
6. The value of the loop emerges most clearly when the system needs to explain why a solution has its current shape.

## What Must Improve

1. The system must detect changes to identifiers and data relationships better.
2. A new prompt must not automatically become a new root if it changes already approved contracts.
3. Local mitigation and strict blocking must be separated.
4. The scorecard should highlight silent architectural drift cases more clearly.
5. Future pilots should define the expected gate behavior before execution.

## Operational Implication

The next evolution should introduce an explicit preference or rule for architectural drift handling.

Possible values:

1. `Mitigate`: current behavior; proceed if the system can reduce the risk.
2. `Review`: pause and ask for confirmation before changing the design.
3. `Strict`: block execution if an identifier, data relationship, invariant, or shared contract changes.

This distinction comes directly from RuleV3 Pilot 3.

## Final Reading

The results show a clear evolution:

1. the first rules demonstrate value on governance and rationale;
2. V2 makes the system more iterative and able to handle local mismatches;
3. V3 improves the tree, detail artifacts, and epistemic guardrails;
4. Pilot 2 shows that V3 produces better evidence against a clean baseline;
5. Pilot 3 reveals the next problem to solve: blocking drift when mitigation is not enough.

Summary:

**C.O.D.E. Loop V3 is already effective as a governance and traceability system. The improvement over previous rules is most visible in the artifact tree, detail files, checkpoints, and truthfulness guardrails. The next leap is to make architectural drift behavior configurable: mitigate, request review, or block.**

## Main References

1. `docs/evaluation/evaluation_scorecard_v0.md`
2. `docs/pilot/pilot_01_comparative_review.md`
3. `docs/pilot/pilot_02_comparative_review.md`
4. `docs/pilot/milestone_4_final_retrospective.md`
5. `docs/decisions/dr-004-v2-checkpoints-and-artifact-branching.md`
6. `docs/decisions/dr-005-v3-artifact-tree-and-guardrails.md`
7. `docs/model/artifact_tree_operating_model_v3.md`
8. `docs/model/operational_guardrails_model_v3.md`
9. `pilot_runs/RuleV2/pilot_3/with_rule/docs/CODE_LOOP_ARTIFACTS.md`
10. `pilot_runs/RuleV3/pilot_2/review/comparative_analysis.md`
11. `pilot_runs/RuleV3/pilot_3/report.md`
12. `future_idee/preference_idea.md`
