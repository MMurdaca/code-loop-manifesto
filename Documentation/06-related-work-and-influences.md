# Related Work And Influences

## A Conceptual Lineage

C.O.D.E. Loop is not an official continuation of any prior methodology.

It is also not a replacement for existing engineering practices.

It is better understood as a response to a new pressure: generative agents can now act inside the software process with enough speed and scope that intent, architecture and validation need a more explicit governance layer.

Several older traditions help explain the shape of that response.

## Program Verification And Formal Methods

Program verification and formal methods introduced a powerful idea: software should be reasoned about before it is trusted.

Work by Robert W. Floyd and C. A. R. Hoare helped establish ways of thinking about programs through assertions, preconditions, postconditions and correctness arguments.

C.O.D.E. Loop is not a formal methods system.

It does not claim mathematical proof of correctness.

But it inherits a related concern: before execution becomes authoritative, the system should have an explicit representation of what must be true.

## Model Checking

Model checking made another idea visible: a model can be checked against desired properties.

The connection to C.O.D.E. Loop is conceptual, not technical.

C.O.D.E. Loop does not explore finite states or replace model checking tools.

It borrows the discipline of refusing to treat execution as the only place where correctness can be evaluated.

## Autonomic Computing And Control Loops

Autonomic computing, including the MAPE-K tradition, is relevant because it treats complex systems through control loops.

Monitor, Analyze, Plan and Execute describe a pattern of observing state, interpreting it, choosing a response and acting.

C.O.D.E. Loop applies control-loop thinking to a different target.

It is not primarily about running infrastructure.

It is about governing the cognitive path from intent to implementation.

The analogy is useful, but it should not be overstated.

MAPE-K governs adaptive systems in operation. C.O.D.E. Loop governs software work before and during implementation.

## Agile, XP And TDD

Agile, Extreme Programming and Test-Driven Development made feedback central to modern software practice.

TDD in particular gave developers a compact discipline:

```text
Red -> Green -> Refactor
```

This remains valuable.

C.O.D.E. Loop operates at a different level.

TDD asks whether the software is being built correctly against tests.

C.O.D.E. Loop asks whether the work is still building the correct software according to intent, constraints and design rationale.

The two approaches are compatible.

In a C.O.D.E. Loop workflow, TDD belongs naturally inside Execution and validation strategy.

## Continuous Integration And DevOps

Continuous Integration and DevOps changed how software moves through teams and environments.

They made feedback faster, integration safer and delivery more automated.

C.O.D.E. Loop does not replace that pipeline.

It complements it upstream.

CI and DevOps help answer:

```text
Can this change be integrated, tested and delivered reliably?
```

C.O.D.E. Loop asks:

```text
Should this change exist in this form, under this intent, with these constraints?
```

Both questions matter.

## Agentic AI Loops

Agentic AI systems make the problem concrete.

Recent LLM-based systems can reason, call tools, inspect errors, modify files, run tests and iterate toward task completion.

That capability is useful.

It also increases the need for governance.

If an agent can act, the project must define:

1. what the agent is allowed to decide;
2. which artifact it is modifying;
3. what evidence it must produce;
4. when it must stop and escalate;
5. which layer has authority over the current decision.

C.O.D.E. Loop is a proposal for making those boundaries explicit.

## The Gap

The gap C.O.D.E. Loop addresses is not the absence of tools.

It is the absence of a shared operating model for preserving intent while generative systems produce implementation.

Formal methods emphasize proof but are often too heavy for everyday AI-assisted development.

TDD and CI validate behavior but do not fully govern architectural intent.

DevOps accelerates delivery but does not define the cognitive chain behind a change.

Agentic loops can execute, but execution alone does not establish authority.

C.O.D.E. Loop fills this gap by making intent, artifacts, validation and propagation explicit.

