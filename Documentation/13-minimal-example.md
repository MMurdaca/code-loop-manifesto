# Minimal Example

This example shows C.O.D.E. Loop applied to a small feature in Standard Mode.

The goal is not to show every possible artifact field.

The goal is to show the shape of the reasoning.

For smaller changes, Tiny Mode may be enough. For contract, identity, audit or architectural changes, use Strict Mode. See `15-adoption-modes.md`.

## Scenario

Add a small in-memory cache to a service.

The cache should:

1. store values by key;
2. support optional time-to-live;
3. evict expired entries;
4. expose simple hit and miss metrics;
5. avoid external dependencies.

## 1. Concept Artifact

```text
Artifact ID: CONCEPT-CACHE-001
Layer: Concept
Status: Ready for Validation

Problem:
The service repeats expensive lookups and needs a small local cache.

Objectives:
1. Reduce repeated lookup cost.
2. Keep behavior predictable and easy to test.
3. Avoid external services or dependencies.

Constraints:
1. In-memory only.
2. No persistence.
3. No distributed invalidation.
4. No background thread required.

Assumptions:
1. Cache size is small enough for process memory.
2. Time-to-live can be checked lazily on access.

Success Criteria:
1. Values can be stored and retrieved by key.
2. Expired values are not returned.
3. Hit and miss counters are visible.
4. Unit tests cover expiration and metrics.

Out Of Scope:
1. Redis or external cache integration.
2. Multi-process consistency.
3. Advanced eviction algorithms.
```

## 2. Orchestration Artifact

```text
Artifact ID: ORCH-CACHE-001
Layer: Orchestration
Parent: CONCEPT-CACHE-001
Status: Ready for Validation

Work Units:
1. Cache API.
2. Entry storage and expiration.
3. Metrics tracking.
4. Unit tests.

Dependencies:
1. Expiration behavior affects retrieval.
2. Metrics depend on retrieval outcome.
3. Tests must cover both fresh and expired entries.

Sequencing:
1. Define public API.
2. Implement storage and expiration.
3. Add metrics.
4. Add tests.

Risks:
1. Ambiguous behavior for expired entries.
2. Metrics may count expired hits incorrectly.
```

## 3. Design Artifact

```text
Artifact ID: DESIGN-CACHE-001
Layer: Design
Parent: ORCH-CACHE-001
Status: Ready for Validation

Interface:
1. set(key, value, ttl_seconds=None)
2. get(key)
3. delete(key)
4. clear()
5. stats()

Invariants:
1. get(key) returns None if the key is missing.
2. get(key) returns None if the entry is expired.
3. Expired entries are removed lazily when accessed.
4. A fresh successful get increments hits.
5. A missing or expired get increments misses.

Edge Cases:
1. ttl_seconds=None means no expiration.
2. ttl_seconds <= 0 should be rejected or treated as immediate expiration.
3. delete on missing key should be safe.

Validation Strategy:
1. Test set/get.
2. Test missing key.
3. Test expiration.
4. Test metrics.
5. Test delete and clear.

Open Design Decision:
ttl_seconds <= 0 needs explicit choice before implementation.
```

## 4. Escalation Example

The Design layer found an ambiguity:

```text
Clarification Request:
Should ttl_seconds <= 0 be rejected, or should it create an immediately expired entry?

Impact:
This changes API behavior and tests.

Proposed Decision:
Reject ttl_seconds <= 0 with ValueError because it makes invalid caller behavior explicit.
```

After approval, the Design artifact is updated:

```text
Decision:
ttl_seconds <= 0 raises ValueError.
```

## 5. Execution Artifact

```text
Artifact ID: EXEC-CACHE-001
Layer: Execution
Parent: DESIGN-CACHE-001
Status: Ready for Validation

Implemented Scope:
1. Cache API.
2. Lazy expiration.
3. Hit and miss metrics.
4. Unit tests for main behavior.

Validation Evidence:
1. set/get test passed.
2. missing key test passed.
3. expiration test passed.
4. metrics test passed.
5. invalid ttl test passed.

Deviation Notes:
None.

Detected Mismatches:
None.
```

## 6. Validation Report

```text
Artifact ID: VALIDATION-CACHE-001
Layer: Validation
Parent: EXEC-CACHE-001
Status: Pass

Result:
Pass.

Reason:
Execution matches the approved Design.
Design satisfies the Orchestration.
Orchestration preserves the Concept.

Conditions:
None.
```

## What This Example Shows

The loop did not make the feature complicated.

It made the decision path visible.

The important moment was not the code itself. The important moment was catching the ambiguous TTL behavior before implementation silently chose one interpretation.
