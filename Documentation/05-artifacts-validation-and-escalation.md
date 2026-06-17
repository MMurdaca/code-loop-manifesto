# Artifacts, Validation And Escalation

## Conversation Can Explore; Artifacts Govern

Conversation is useful.

It is where ideas are discovered, alternatives are tested and ambiguity is often first exposed.

But conversation is a poor long-term memory for a software project. It is easy to lose. It is hard to review. It does not always survive tool boundaries, agent sessions or team changes.

C.O.D.E. Loop treats artifacts as the operational memory of the work.

An artifact is any explicit, reviewable object that captures the state, decision or output of a layer.

It can be Markdown, JSON, YAML, an issue, a database record, a DSL or another structured representation.

The format is not the point.

The point is that the decision can be read, validated and propagated without relying on hidden context.

## Minimum Artifact Expectations

A useful artifact should answer a few basic questions:

1. What is this artifact about?
2. Which upstream artifact or intent does it depend on?
3. What decisions does it make?
4. What constraints does it preserve?
5. What assumptions does it rely on?
6. What remains uncertain?
7. What evidence supports it?
8. What validation state does it have?

The artifact does not need to be long.

It needs to be clear enough that a human or agent can continue the work without guessing what was meant.

## Validation Gates

An artifact does not become authoritative merely because it exists.

It becomes usable downstream after validation.

C.O.D.E. Loop uses three basic validation outcomes:

1. Pass;
2. Pass with Conditions;
3. Fail.

Pass means the artifact is sufficient for downstream work.

Pass with Conditions means downstream work can continue, but the remaining conditions must be visible and bounded.

Fail means the artifact should not propagate until the issue is resolved.

## Controlled Propagation

Controlled propagation means that each layer consumes only artifacts that are explicit enough and validated enough for the next layer to use.

The downstream layer should know:

1. which artifact it is consuming;
2. which version or state is valid;
3. which constraints must be preserved;
4. which conditions remain open;
5. when it must stop and escalate.

This matters because AI agents are very good at filling gaps.

That strength becomes a weakness when the gap is architectural, contractual or semantic.

C.O.D.E. Loop does not ask agents to stop thinking.

It asks them to distinguish between implementing within authority and changing the authority itself.

## Escalation

Escalation is how information moves upward without creating silent drift.

Escalation is required when:

1. an upstream artifact is ambiguous on a critical point;
2. two active artifacts conflict;
3. downstream work cannot continue without reinterpreting intent;
4. execution reveals a mismatch with design;
5. a local improvement would change scope, constraints or success criteria;
6. a validation condition is no longer sustainable.

Escalation should be explicit, but it does not need to be theatrical.

It should identify:

1. the issue;
2. the affected artifact;
3. the evidence;
4. the impact;
5. the proposed decision or options.

## Types Of Requests

C.O.D.E. Loop uses four basic request types.

Clarification Request:

used when the upstream artifact is not clear enough to proceed.

Change Request:

used when a lower layer proposes a change to an upstream artifact.

Exception Request:

used when a layer asks to operate outside the default rule for a bounded reason.

Re-validation Request:

used when an artifact that was previously valid needs to be reviewed again because new evidence has appeared.

## Branches And Artifact Trees

Larger work often cannot be governed as one linear chain.

In those cases, a parent artifact may produce multiple child artifacts.

This creates an artifact tree.

Each child should declare:

1. its parent;
2. the scope it covers;
3. its dependencies;
4. its validation state;
5. whether the parent still has deferred or uncovered scope.

The purpose of an artifact tree is not to create more paperwork.

The purpose is to keep lineage visible as the work becomes more detailed.

